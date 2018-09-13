---
title: Azure Search Service REST API Version 2015-02-28-Preview | Microsoft Docs
description: Azure Search Service REST API Version 2015-02-28-Preview includes experimental features such as Natural Language Analyzers and moreLikeThis searches.
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: ''
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 09/07/2016
ms.author: brjohnst
ms.openlocfilehash: 34532b0948e210aca6e2d9364581008d74d22faa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562955"
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="2fa7a-103">Azure Search Service REST API: Version 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="2fa7a-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="2fa7a-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="2fa7a-107">It finds other documents that are relevant to another specific document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="2fa7a-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="2fa7a-109">These include:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-109">These include:</span></span>

* [<span data-ttu-id="2fa7a-110">Scoring Profiles</span><span class="sxs-lookup"><span data-stu-id="2fa7a-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="2fa7a-111">Indexers</span><span class="sxs-lookup"><span data-stu-id="2fa7a-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="2fa7a-112">Azure Search service is available in multiple versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="2fa7a-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="2fa7a-114">APIs in this document</span><span class="sxs-lookup"><span data-stu-id="2fa7a-114">APIs in this document</span></span>
<span data-ttu-id="2fa7a-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="2fa7a-116">The following list shows the simple syntax.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="2fa7a-117">Create Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-118">Update Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-119">Get Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-120">Listing Indexes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-121">Get Index Statistics</span><span class="sxs-lookup"><span data-stu-id="2fa7a-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-122">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="2fa7a-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-123">Delete an Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-124">Add, Delete, and Update Data within an Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-125">Search Documents</span><span class="sxs-lookup"><span data-stu-id="2fa7a-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-126">Lookup Document</span><span class="sxs-lookup"><span data-stu-id="2fa7a-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="2fa7a-127">Count Documents</span><span class="sxs-lookup"><span data-stu-id="2fa7a-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="2fa7a-128">Suggestions</span><span class="sxs-lookup"><span data-stu-id="2fa7a-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="2fa7a-129">Index Operations</span><span class="sxs-lookup"><span data-stu-id="2fa7a-129">Index Operations</span></span>
<span data-ttu-id="2fa7a-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="2fa7a-131">To create an index, you first POST a JSON document that describes the index schema.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="2fa7a-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="2fa7a-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="2fa7a-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="2fa7a-135">Notice how attributes control how the field is used.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="2fa7a-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="2fa7a-137">After the index is created, you'll upload documents that populate the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="2fa7a-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="2fa7a-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="2fa7a-140">Create Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-140">Create Index</span></span>
<span data-ttu-id="2fa7a-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="2fa7a-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="2fa7a-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="2fa7a-144">The body of the request is a JSON schema that specifies the index and configuration information.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="2fa7a-145">Alternatively, you can use PUT and specify the index name on the URI.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="2fa7a-146">If the index does not exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="2fa7a-147">Creating an index determines the structure of the documents stored and used in search operations.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="2fa7a-148">Populating the index is a separate operation.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="2fa7a-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="2fa7a-150">The inverted index is generated when the documents are posted.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="2fa7a-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="2fa7a-152">The free service allows up to 3 indexes.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="2fa7a-153">Standard service allows 50 indexes per Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="2fa7a-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="2fa7a-155">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-155">**Request**</span></span>

<span data-ttu-id="2fa7a-156">HTTPS is required for all service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="2fa7a-157">The **Create Index** request can be constructed using either a POST or PUT method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="2fa7a-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="2fa7a-159">With PUT, the index name is part of the URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="2fa7a-160">If the index doesn't exist, it is created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="2fa7a-161">If it already exists, it is updated to the new definition.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="2fa7a-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="2fa7a-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="2fa7a-164">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-164">The `api-version` is required.</span></span> <span data-ttu-id="2fa7a-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="2fa7a-166">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-166">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-167">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-168">`Content-Type`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-168">`Content-Type`: Required.</span></span> <span data-ttu-id="2fa7a-169">Set this to `application/json`</span><span class="sxs-lookup"><span data-stu-id="2fa7a-169">Set this to `application/json`</span></span>
* <span data-ttu-id="2fa7a-170">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-170">`api-key`: Required.</span></span> <span data-ttu-id="2fa7a-171">The `api-key` is used to</span><span class="sxs-lookup"><span data-stu-id="2fa7a-171">The `api-key` is used to</span></span>
* <span data-ttu-id="2fa7a-172">authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-173">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-175">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<a name="RequestData"></a>
<span data-ttu-id="2fa7a-178">**Request Body Syntax**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-178">**Request Body Syntax**</span></span>

<span data-ttu-id="2fa7a-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="2fa7a-180">Note that for a POST request, you must specify the index name in the request body.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="2fa7a-181">There can only be one key field in the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-181">There can only be one key field in the index.</span></span> <span data-ttu-id="2fa7a-182">It has to be a string field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-182">It has to be a string field.</span></span> <span data-ttu-id="2fa7a-183">This field represents the unique identifier for each document stored within the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="2fa7a-184">The main parts of an index include the following:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="2fa7a-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="2fa7a-186">`suggesters` used for auto-complete or type-ahead queries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="2fa7a-187">`scoringProfiles` used for custom search score ranking.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="2fa7a-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="2fa7a-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="2fa7a-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="2fa7a-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="2fa7a-192">`corsOptions` to allow cross-origin queries against your index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="2fa7a-193">The syntax for structuring the request payload is as follows.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="2fa7a-194">A sample request is provided further on in this topic.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="2fa7a-195">**Index Attributes**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-195">**Index Attributes**</span></span>

<span data-ttu-id="2fa7a-196">The following attributes can be set when creating an index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="2fa7a-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="2fa7a-198">`name` - Sets the name of the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="2fa7a-199">`type` - Sets the data type for the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-199">`type` - Sets the data type for the field.</span></span> <span data-ttu-id="2fa7a-200">See [Supported Data Types](#DataTypes) for a list of supported types.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-200">See [Supported Data Types](#DataTypes) for a list of supported types.</span></span>

<span data-ttu-id="2fa7a-201">`searchable` - Marks the field as full-text search-able.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-201">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="2fa7a-202">This means it will undergo analysis such as word-breaking during indexing.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-202">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="2fa7a-203">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-203">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="2fa7a-204">This enables full-text searches for these terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-204">This enables full-text searches for these terms.</span></span> <span data-ttu-id="2fa7a-205">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-205">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="2fa7a-206">Fields of other types cannot be `searchable`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-206">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="2fa7a-207">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-207">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="2fa7a-208">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-208">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="2fa7a-209">`filterable` - Allows the field to be referenced in `$filter` queries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-209">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="2fa7a-210">`filterable` differs from `searchable` in how strings are handled.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-210">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="2fa7a-211">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-211">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="2fa7a-212">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-212">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="2fa7a-213">All fields are `filterable` by default.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-213">All fields are `filterable` by default.</span></span>

<span data-ttu-id="2fa7a-214">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-214">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="2fa7a-215">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-215">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="2fa7a-216">All other fields are `sortable` by default.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-216">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="2fa7a-217">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-217">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="2fa7a-218">This option cannot be used with fields of type `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-218">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="2fa7a-219">All other fields are `facetable` by default.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-219">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="2fa7a-220">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-220">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="2fa7a-221">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-221">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="2fa7a-222">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-222">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="2fa7a-223">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-223">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="2fa7a-224">This option is useful for fields that are not used in queries, but are needed in search results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-224">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="2fa7a-225">Excluding such fields from the index improves performance.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-225">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="2fa7a-226">`key` - Marks the field as containing unique identifiers for documents within the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-226">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="2fa7a-227">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-227">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="2fa7a-228">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-228">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="2fa7a-229">`retrievable` - Sets whether the field can be returned in a search result.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-229">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="2fa7a-230">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-230">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="2fa7a-231">This attribute must be `true` for `key` fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-231">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="2fa7a-232">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-232">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="2fa7a-233">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-233">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="2fa7a-234">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-234">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="2fa7a-235">Once the analyzer is chosen, it cannot be changed for the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-235">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="2fa7a-236">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-236">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="2fa7a-237">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-237">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="2fa7a-238">This option can be used only with `searchable` fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-238">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="2fa7a-239">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-239">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="2fa7a-240">This analyzer can be updated on an existing field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-240">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="2fa7a-241">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-241">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="2fa7a-242">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-242">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="2fa7a-243">This option can be used only with `searchable` fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-243">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="2fa7a-244">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-244">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="2fa7a-245">Once the analyzer is chosen, it cannot be changed for the field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-245">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="2fa7a-246">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-246">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="2fa7a-247">See [Suggesters](#Suggesters) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-247">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="2fa7a-248">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-248">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="2fa7a-249">Scoring profiles are made up of field weights and functions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-249">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="2fa7a-250">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-250">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="2fa7a-251"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-251"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="2fa7a-252">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-252">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="2fa7a-253">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-253">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="2fa7a-254">Additionally, the standard analyzer converts all characters to their lower case form.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-254">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="2fa7a-255">Both indexed documents and search terms go through the analysis during indexing and query processing.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-255">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="2fa7a-256">Azure Search supports a variety of languages.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-256">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="2fa7a-257">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-257">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="2fa7a-258">Azure Search offers two types of analyzers:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-258">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="2fa7a-259">35 analyzers backed by Lucene.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-259">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="2fa7a-260">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-260">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="2fa7a-261">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-261">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="2fa7a-262">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-262">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="2fa7a-263">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-263">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="2fa7a-264">***How they compare***</span><span class="sxs-lookup"><span data-stu-id="2fa7a-264">***How they compare***</span></span>

<span data-ttu-id="2fa7a-265">The Lucene analyzer for English extends the standard analyzer.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-265">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="2fa7a-266">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-266">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="2fa7a-267">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-267">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="2fa7a-268">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-268">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="2fa7a-269">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-269">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="2fa7a-270">Search performance should not be significantly affected for average size queries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-270">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="2fa7a-271">***Configuration***</span><span class="sxs-lookup"><span data-stu-id="2fa7a-271">***Configuration***</span></span>

<span data-ttu-id="2fa7a-272">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-272">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="2fa7a-273">The same analyzer will be applied when indexing and searching for that field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-273">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="2fa7a-274">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-274">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="2fa7a-275">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-275">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="2fa7a-276">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-276">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="2fa7a-277">***Analyzer list***</span><span class="sxs-lookup"><span data-stu-id="2fa7a-277">***Analyzer list***</span></span>

<span data-ttu-id="2fa7a-278">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-278">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="2fa7a-279">Language</span><span class="sxs-lookup"><span data-stu-id="2fa7a-279">Language</span></span></th>
        <th><span data-ttu-id="2fa7a-280">Microsoft analyzer name</span><span class="sxs-lookup"><span data-stu-id="2fa7a-280">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="2fa7a-281">Lucene analyzer name</span><span class="sxs-lookup"><span data-stu-id="2fa7a-281">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-282">Arabic</span><span class="sxs-lookup"><span data-stu-id="2fa7a-282">Arabic</span></span></td>
        <td><span data-ttu-id="2fa7a-283">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-283">ar.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-284">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-284">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-285">Armenian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-285">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="2fa7a-286">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-286">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-287">Bangla</span><span class="sxs-lookup"><span data-stu-id="2fa7a-287">Bangla</span></span></td>
        <td><span data-ttu-id="2fa7a-288">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-288">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="2fa7a-289">Basque</span><span class="sxs-lookup"><span data-stu-id="2fa7a-289">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="2fa7a-290">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-290">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="2fa7a-291">Bulgarian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-291">Bulgarian</span></span></td>
        <td><span data-ttu-id="2fa7a-292">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-292">bg.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-293">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-293">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="2fa7a-294">Catalan</span><span class="sxs-lookup"><span data-stu-id="2fa7a-294">Catalan</span></span></td>
        <td><span data-ttu-id="2fa7a-295">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-295">ca.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-296">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-296">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-297">Chinese Simplified</span><span class="sxs-lookup"><span data-stu-id="2fa7a-297">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="2fa7a-298">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-298">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-299">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-299">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-300">Chinese Traditional</span><span class="sxs-lookup"><span data-stu-id="2fa7a-300">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="2fa7a-301">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-301">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-302">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-302">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="2fa7a-303">Croatian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-303">Croatian</span></span></td>
        <td><span data-ttu-id="2fa7a-304">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-304">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-305">Czech</span><span class="sxs-lookup"><span data-stu-id="2fa7a-305">Czech</span></span></td>
        <td><span data-ttu-id="2fa7a-306">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-306">cs.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-307">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-307">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="2fa7a-308">Danish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-308">Danish</span></span></td>
        <td><span data-ttu-id="2fa7a-309">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-309">da.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-310">da.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-310">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="2fa7a-311">Dutch</span><span class="sxs-lookup"><span data-stu-id="2fa7a-311">Dutch</span></span></td>
        <td><span data-ttu-id="2fa7a-312">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-312">nl.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-313">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-313">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="2fa7a-314">English</span><span class="sxs-lookup"><span data-stu-id="2fa7a-314">English</span></span></td>        
        <td><span data-ttu-id="2fa7a-315">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-315">en.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-316">en.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-316">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-317">Estonian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-317">Estonian</span></span></td>
        <td><span data-ttu-id="2fa7a-318">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-318">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-319">Finnish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-319">Finnish</span></span></td>
        <td><span data-ttu-id="2fa7a-320">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-320">fi.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-321">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-321">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="2fa7a-322">French</span><span class="sxs-lookup"><span data-stu-id="2fa7a-322">French</span></span></td>
        <td><span data-ttu-id="2fa7a-323">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-323">fr.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-324">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-324">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-325">Galician</span><span class="sxs-lookup"><span data-stu-id="2fa7a-325">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="2fa7a-326">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-326">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-327">German</span><span class="sxs-lookup"><span data-stu-id="2fa7a-327">German</span></span></td>
        <td><span data-ttu-id="2fa7a-328">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-328">de.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-329">de.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-329">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-330">Greek</span><span class="sxs-lookup"><span data-stu-id="2fa7a-330">Greek</span></span></td>
        <td><span data-ttu-id="2fa7a-331">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-331">el.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-332">el.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-332">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-333">Gujarati</span><span class="sxs-lookup"><span data-stu-id="2fa7a-333">Gujarati</span></span></td>
        <td><span data-ttu-id="2fa7a-334">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-334">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-335">Hebrew</span><span class="sxs-lookup"><span data-stu-id="2fa7a-335">Hebrew</span></span></td>
        <td><span data-ttu-id="2fa7a-336">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-336">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-337">Hindi</span><span class="sxs-lookup"><span data-stu-id="2fa7a-337">Hindi</span></span></td>
        <td><span data-ttu-id="2fa7a-338">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-338">hi.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-339">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-339">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-340">Hungarian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-340">Hungarian</span></span></td>        
        <td><span data-ttu-id="2fa7a-341">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-341">hu.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-342">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-342">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-343">Icelandic</span><span class="sxs-lookup"><span data-stu-id="2fa7a-343">Icelandic</span></span></td>
        <td><span data-ttu-id="2fa7a-344">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-344">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-345">Indonesian (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-345">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="2fa7a-346">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-346">id.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-347">id.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-347">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-348">Irish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-348">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="2fa7a-349">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-349">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-350">Italian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-350">Italian</span></span></td>
        <td><span data-ttu-id="2fa7a-351">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-351">it.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-352">it.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-352">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-353">Japanese</span><span class="sxs-lookup"><span data-stu-id="2fa7a-353">Japanese</span></span></td>
        <td><span data-ttu-id="2fa7a-354">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-354">ja.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-355">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-355">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-356">Kannada</span><span class="sxs-lookup"><span data-stu-id="2fa7a-356">Kannada</span></span></td>
        <td><span data-ttu-id="2fa7a-357">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-357">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-358">Korean</span><span class="sxs-lookup"><span data-stu-id="2fa7a-358">Korean</span></span></td>
        <td><span data-ttu-id="2fa7a-359">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-359">ko.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-360">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-360">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-361">Latvian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-361">Latvian</span></span></td>        
        <td><span data-ttu-id="2fa7a-362">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-362">lv.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-363">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-363">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-364">Lithuanian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-364">Lithuanian</span></span></td>
        <td><span data-ttu-id="2fa7a-365">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-365">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-366">Malayalam</span><span class="sxs-lookup"><span data-stu-id="2fa7a-366">Malayalam</span></span></td>
        <td><span data-ttu-id="2fa7a-367">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-367">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-368">Malay (Latin)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-368">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="2fa7a-369">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-369">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-370">Marathi</span><span class="sxs-lookup"><span data-stu-id="2fa7a-370">Marathi</span></span></td>
        <td><span data-ttu-id="2fa7a-371">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-371">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-372">Norwegian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-372">Norwegian</span></span></td>
        <td><span data-ttu-id="2fa7a-373">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-373">nb.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-374">no.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-374">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="2fa7a-375">Persian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-375">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="2fa7a-376">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-376">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-377">Polish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-377">Polish</span></span></td>
        <td><span data-ttu-id="2fa7a-378">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-378">pl.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-379">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-379">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-380">Portuguese (Brazil)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-380">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="2fa7a-381">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-381">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-382">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-382">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-383">Portuguese (Portugal)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-383">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="2fa7a-384">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-384">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="2fa7a-385">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-385">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-386">Punjabi</span><span class="sxs-lookup"><span data-stu-id="2fa7a-386">Punjabi</span></span></td>
        <td><span data-ttu-id="2fa7a-387">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-387">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-388">Romanian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-388">Romanian</span></span></td>
        <td><span data-ttu-id="2fa7a-389">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-389">ro.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-390">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-390">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-391">Russian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-391">Russian</span></span></td>
        <td><span data-ttu-id="2fa7a-392">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-392">ru.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-393">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-393">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-394">Serbian (Cyrillic)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-394">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="2fa7a-395">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-395">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-396">Serbian (Latin)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-396">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="2fa7a-397">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-397">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-398">Slovak</span><span class="sxs-lookup"><span data-stu-id="2fa7a-398">Slovak</span></span></td>
        <td><span data-ttu-id="2fa7a-399">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-399">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-400">Slovenian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-400">Slovenian</span></span></td>
        <td><span data-ttu-id="2fa7a-401">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-401">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-402">Spanish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-402">Spanish</span></span></td>
        <td><span data-ttu-id="2fa7a-403">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-403">es.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-404">es.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-404">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-405">Swedish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-405">Swedish</span></span></td>
        <td><span data-ttu-id="2fa7a-406">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-406">sv.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-407">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-407">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="2fa7a-408">Tamil</span><span class="sxs-lookup"><span data-stu-id="2fa7a-408">Tamil</span></span></td>
        <td><span data-ttu-id="2fa7a-409">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-409">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-410">Telugu</span><span class="sxs-lookup"><span data-stu-id="2fa7a-410">Telugu</span></span></td>
        <td><span data-ttu-id="2fa7a-411">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-411">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-412">Thai</span><span class="sxs-lookup"><span data-stu-id="2fa7a-412">Thai</span></span></td>
        <td><span data-ttu-id="2fa7a-413">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-413">th.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-414">th.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-414">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-415">Turkish</span><span class="sxs-lookup"><span data-stu-id="2fa7a-415">Turkish</span></span></td>
        <td><span data-ttu-id="2fa7a-416">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-416">tr.microsoft</span></span></td>
        <td><span data-ttu-id="2fa7a-417">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-417">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-418">Ukrainian</span><span class="sxs-lookup"><span data-stu-id="2fa7a-418">Ukrainian</span></span></td>
        <td><span data-ttu-id="2fa7a-419">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-419">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-420">Urdu</span><span class="sxs-lookup"><span data-stu-id="2fa7a-420">Urdu</span></span></td>
        <td><span data-ttu-id="2fa7a-421">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-421">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-422">Vietnamese</span><span class="sxs-lookup"><span data-stu-id="2fa7a-422">Vietnamese</span></span></td>
        <td><span data-ttu-id="2fa7a-423">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="2fa7a-423">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="2fa7a-424">Additionally Azure Search provides language-agnostic analyzer configurations</span><span class="sxs-lookup"><span data-stu-id="2fa7a-424">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="2fa7a-425">Standard ASCII Folding</span><span class="sxs-lookup"><span data-stu-id="2fa7a-425">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="2fa7a-426">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="2fa7a-426">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="2fa7a-427">Unicode text segmentation (Standard Tokenizer)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-427">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="2fa7a-428">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-428">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="2fa7a-429">This is useful for removing diacritics.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-429">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="2fa7a-430">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-430">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="2fa7a-431">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-431">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="2fa7a-432">**Suggesters**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-432">**Suggesters**</span></span>

<span data-ttu-id="2fa7a-433">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-433">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="2fa7a-434">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-434">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="2fa7a-435">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-435">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="2fa7a-436">See [Suggesters](#Suggesters) for configuration details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-436">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="2fa7a-437">**Scoring profiles**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-437">**Scoring profiles**</span></span>

<span data-ttu-id="2fa7a-438">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-438">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="2fa7a-439">Scoring profiles are made up of field weights and functions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-439">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="2fa7a-440">To use them, you specify a profile by name on the query string.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-440">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="2fa7a-441">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-441">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="2fa7a-442">You can use the internal, unnamed scoring profile.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-442">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="2fa7a-443">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-443">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="2fa7a-444">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-444">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="2fa7a-445">**CORS Options**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-445">**CORS Options**</span></span>

<span data-ttu-id="2fa7a-446">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-446">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="2fa7a-447">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-447">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="2fa7a-448">Note that only query APIs support CORS for security reasons.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-448">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="2fa7a-449">The following options can be set for CORS:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-449">The following options can be set for CORS:</span></span>

* <span data-ttu-id="2fa7a-450">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-450">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="2fa7a-451">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-451">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="2fa7a-452">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-452">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="2fa7a-453">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-453">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="2fa7a-454">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-454">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="2fa7a-455">Note that **this is not recommended practice for production search services.**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-455">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="2fa7a-456">However, it may be useful for development or debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-456">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="2fa7a-457">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-457">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="2fa7a-458">This must be a non-negative integer.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-458">This must be a non-negative integer.</span></span> <span data-ttu-id="2fa7a-459">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-459">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="2fa7a-460">If it is not set, a default duration of 5 minutes will be used.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-460">If it is not set, a default duration of 5 minutes will be used.</span></span>

<a name="CreateUpdateIndexExample"></a>
<span data-ttu-id="2fa7a-461">**Request Body Example**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-461">**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="2fa7a-462">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-462">**Response**</span></span>

<span data-ttu-id="2fa7a-463">For a successful request: "201 Created".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-463">For a successful request: "201 Created".</span></span>

<span data-ttu-id="2fa7a-464">By default the response body will contain the JSON for the index definition that was created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-464">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="2fa7a-465">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-465">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="2fa7a-466">This is true regardless of whether PUT or POST was used to create the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-466">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="2fa7a-467">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-467">**Remarks**</span></span>

<span data-ttu-id="2fa7a-468">Currently, there is limited support for index schema updates.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-468">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="2fa7a-469">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-469">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="2fa7a-470">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-470">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="2fa7a-471">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-471">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="2fa7a-472">No additional storage space will be consumed until new documents are added to the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-472">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="2fa7a-473">Suggesters</span><span class="sxs-lookup"><span data-stu-id="2fa7a-473">Suggesters</span></span>
<span data-ttu-id="2fa7a-474">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-474">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="2fa7a-475">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-475">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="2fa7a-476">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-476">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="2fa7a-477">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-477">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="2fa7a-478">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-478">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="2fa7a-479">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-479">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="2fa7a-480">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-480">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="2fa7a-481">This article explains how to configure a **suggester**.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-481">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="2fa7a-482">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-482">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="2fa7a-483">**Usage**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-483">**Usage**</span></span>

<span data-ttu-id="2fa7a-484">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-484">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="2fa7a-485">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-485">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="2fa7a-486">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-486">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="2fa7a-487">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-487">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="2fa7a-488">Properties that define a suggester include the following:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-488">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="2fa7a-489">`name`: The name of the suggester.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-489">`name`: The name of the suggester.</span></span> <span data-ttu-id="2fa7a-490">You use the name of the suggester when calling the `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-490">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="2fa7a-491">`searchMode`: The strategy used to search for candidate phrases.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-491">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="2fa7a-492">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-492">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="2fa7a-493">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-493">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="2fa7a-494">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-494">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="2fa7a-495">Only fields that don't have a custom language analyzer set can be used.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-495">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="2fa7a-496">**Suggester Example**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-496">**Suggester Example**</span></span>

<span data-ttu-id="2fa7a-497">A suggester is part of the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-497">A suggester is part of the index.</span></span> <span data-ttu-id="2fa7a-498">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-498">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="2fa7a-499">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-499">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="2fa7a-500">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-500">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="2fa7a-501">Starting with the generally available release, this is now the only implementation of the suggestions API.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-501">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="2fa7a-502">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-502">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="2fa7a-503">Update Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-503">Update Index</span></span>
<span data-ttu-id="2fa7a-504">You can update an existing index within Azure Search using an HTTP PUT request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-504">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="2fa7a-505">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-505">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="2fa7a-506">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-506">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="2fa7a-507">You specify the name of the index to update on the request URI:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-507">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="2fa7a-508">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-508">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="2fa7a-509">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-509">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="2fa7a-510">New fields can be added at any time, although existing fields cannot be changed or deleted.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-510">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="2fa7a-511">The same applies to `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-511">The same applies to `suggesters`.</span></span> <span data-ttu-id="2fa7a-512">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-512">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="2fa7a-513">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-513">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="2fa7a-514">No additional storage space will be consumed until new documents are added to the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-514">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="2fa7a-515">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-515">**Request**</span></span>

<span data-ttu-id="2fa7a-516">HTTPS is required for all service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-516">HTTPS is required for all service requests.</span></span> <span data-ttu-id="2fa7a-517">The **Update Index** request is constructed using HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-517">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="2fa7a-518">With PUT, the index name is part of the URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-518">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="2fa7a-519">If the index doesn't exist, it is created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-519">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="2fa7a-520">If the index already exists, it is updated to the new definition.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-520">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="2fa7a-521">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-521">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="2fa7a-522">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-522">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="2fa7a-523">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-523">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-524">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-524">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-525">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-525">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-526">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-526">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-527">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-527">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-528">`Content-Type`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-528">`Content-Type`: Required.</span></span> <span data-ttu-id="2fa7a-529">Set this to `application/json`</span><span class="sxs-lookup"><span data-stu-id="2fa7a-529">Set this to `application/json`</span></span>
* <span data-ttu-id="2fa7a-530">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-530">`api-key`: Required.</span></span> <span data-ttu-id="2fa7a-531">The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-531">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-532">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-532">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-533">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-533">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-534">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-534">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-535">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-535">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-536">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-536">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-537">**Request Body Syntax**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-537">**Request Body Syntax**</span></span>

<span data-ttu-id="2fa7a-538">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-538">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="2fa7a-539">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-539">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="2fa7a-540">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-540">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="2fa7a-541">The schema syntax used to create an index is reproduced here for convenience.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-541">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="2fa7a-542">See [Create Index](#CreateIndex) for more details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-542">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="2fa7a-543">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-543">**Response**</span></span>

<span data-ttu-id="2fa7a-544">For a successful request: "204 No Content".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-544">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="2fa7a-545">By default the response body will be empty.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-545">By default the response body will be empty.</span></span> <span data-ttu-id="2fa7a-546">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-546">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="2fa7a-547">In this case, the success status code will be "200 OK".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-547">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="2fa7a-548">**Updating index definition with custom analyzers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-548">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="2fa7a-549">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-549">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="2fa7a-550">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-550">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="2fa7a-551">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-551">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="2fa7a-552">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-552">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="2fa7a-553">List Indexes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-553">List Indexes</span></span>
<span data-ttu-id="2fa7a-554">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-554">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="2fa7a-555">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-555">**Request**</span></span>

<span data-ttu-id="2fa7a-556">HTTPS is required for all service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-556">HTTPS is required for all service requests.</span></span> <span data-ttu-id="2fa7a-557">The **List Indexes** request can be constructed using the GET method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-557">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="2fa7a-558">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-558">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-559">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-559">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-560">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-560">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-561">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-561">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-562">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-562">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-563">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-563">`api-key`: Required.</span></span> <span data-ttu-id="2fa7a-564">The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-564">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-565">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-565">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-566">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-566">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-567">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-567">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-568">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-568">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-569">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-569">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-570">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-570">**Request Body**</span></span>

<span data-ttu-id="2fa7a-571">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-571">None.</span></span>

<span data-ttu-id="2fa7a-572">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-572">**Response**</span></span>

<span data-ttu-id="2fa7a-573">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-573">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="2fa7a-574">Here is an example response body:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-574">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="2fa7a-575">Note that you can filter the response down to just the properties you're interested in.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-575">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="2fa7a-576">For example, if you want only a list of index names, use the OData `$select` query option:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-576">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="2fa7a-577">In this case, the response from the above example would appear as follows:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-577">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="2fa7a-578">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-578">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="2fa7a-579">Get Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-579">Get Index</span></span>
<span data-ttu-id="2fa7a-580">The **Get Index** operation gets the index definition from Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-580">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="2fa7a-581">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-581">**Request**</span></span>

<span data-ttu-id="2fa7a-582">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-582">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-583">The **Get Index** request can be constructed using the GET method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-583">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="2fa7a-584">The [index name] in the request URI specifies which index to return from the indexes collection.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-584">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="2fa7a-585">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-585">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-586">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-586">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-587">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-587">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-588">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-588">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-589">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-589">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-590">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-590">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-591">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-591">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-592">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-592">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-593">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-593">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-594">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-594">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-595">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-595">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-596">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-596">**Request Body**</span></span>

<span data-ttu-id="2fa7a-597">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-597">None.</span></span>

<span data-ttu-id="2fa7a-598">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-598">**Response**</span></span>

<span data-ttu-id="2fa7a-599">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-599">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="2fa7a-600">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-600">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="2fa7a-601">Delete Index</span><span class="sxs-lookup"><span data-stu-id="2fa7a-601">Delete Index</span></span>
<span data-ttu-id="2fa7a-602">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-602">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="2fa7a-603">You can get the index name from the service dashboard in the Azure portal, or from the API.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-603">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="2fa7a-604">See [List Indexes](#ListIndexes) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-604">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="2fa7a-605">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-605">**Request**</span></span>

<span data-ttu-id="2fa7a-606">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-606">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-607">The **Delete Index** request can be constructed using the DELETE method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-607">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="2fa7a-608">The [index name] in the request URI specifies which index to delete from the indexes collection.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-608">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="2fa7a-609">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-609">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-610">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-610">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-611">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-611">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-612">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-612">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-613">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-613">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-614">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-614">`api-key`: Required.</span></span> <span data-ttu-id="2fa7a-615">The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-615">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-616">It is a string value, unique to your service URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-616">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="2fa7a-617">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-617">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-618">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-618">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-619">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-619">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-620">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-620">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-621">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-621">**Request Body**</span></span>

<span data-ttu-id="2fa7a-622">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-622">None.</span></span>

<span data-ttu-id="2fa7a-623">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-623">**Response**</span></span>

<span data-ttu-id="2fa7a-624">Status Code: 204 No Content is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-624">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="2fa7a-625">Get Index Statistics</span><span class="sxs-lookup"><span data-stu-id="2fa7a-625">Get Index Statistics</span></span>
<span data-ttu-id="2fa7a-626">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-626">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="2fa7a-627">Statistics on document count and storage size are collected every few minutes, not in real time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-627">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="2fa7a-628">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-628">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="2fa7a-629">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-629">**Request**</span></span>

<span data-ttu-id="2fa7a-630">HTTPS is required for all services requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-630">HTTPS is required for all services requests.</span></span> <span data-ttu-id="2fa7a-631">The **Get Index Statistics** request can be constructed using the GET method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-631">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="2fa7a-632">The [index name] in the request URI tells the service to return index statistics for the specified index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-632">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="2fa7a-633">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-633">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-634">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-634">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-635">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-635">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-636">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-636">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-637">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-637">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-638">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-638">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-639">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-639">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-640">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-640">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-641">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-641">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-642">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-642">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-643">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-643">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-644">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-644">**Request Body**</span></span>

<span data-ttu-id="2fa7a-645">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-645">None.</span></span>

<span data-ttu-id="2fa7a-646">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-646">**Response**</span></span>

<span data-ttu-id="2fa7a-647">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-647">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="2fa7a-648">The response body is in the following format:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-648">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="2fa7a-649">Test Analyzer</span><span class="sxs-lookup"><span data-stu-id="2fa7a-649">Test Analyzer</span></span>
<span data-ttu-id="2fa7a-650">The **Analyze API** shows how an analyzer breaks text into tokens.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-650">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="2fa7a-651">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-651">**Request**</span></span>

<span data-ttu-id="2fa7a-652">HTTPS is required for all services requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-652">HTTPS is required for all services requests.</span></span> <span data-ttu-id="2fa7a-653">The **Analyze API** request can be constructed using the POST method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-653">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="2fa7a-654">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-654">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-655">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-655">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-656">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-656">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-657">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-657">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-658">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-658">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-659">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-659">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-660">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-660">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-661">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-661">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-662">You will also need the index name and the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-662">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-663">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-663">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-664">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-664">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-665">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-665">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="2fa7a-666">or</span><span class="sxs-lookup"><span data-stu-id="2fa7a-666">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="2fa7a-667">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-667">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="2fa7a-668">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-668">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="2fa7a-669">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-669">**Response**</span></span>

<span data-ttu-id="2fa7a-670">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-670">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="2fa7a-671">The response body is in the following format:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-671">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="2fa7a-672">**Analyze API example**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-672">**Analyze API example**</span></span>

<span data-ttu-id="2fa7a-673">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-673">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="2fa7a-674">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-674">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="2fa7a-675">Document Operations</span><span class="sxs-lookup"><span data-stu-id="2fa7a-675">Document Operations</span></span>
<span data-ttu-id="2fa7a-676">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-676">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="2fa7a-677">All the documents that you upload comprise the corpus of your search data.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-677">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="2fa7a-678">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-678">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="2fa7a-679">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-679">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="2fa7a-680">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-680">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="2fa7a-681">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-681">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or DocumentDB.</span></span> <span data-ttu-id="2fa7a-682">Typically, indexes are populated from a single dataset that you provide.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-682">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="2fa7a-683">You should plan on having one document for each item that you want to search.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-683">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="2fa7a-684">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-684">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="2fa7a-685">Documents consist of one or more fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-685">Documents consist of one or more fields.</span></span> <span data-ttu-id="2fa7a-686">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-686">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="2fa7a-687">The names, data types, and search features supported for each field are determined by the index schema.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-687">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="2fa7a-688">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-688">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="2fa7a-689">All other document fields are optional and will default to a null value if left unspecified.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-689">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="2fa7a-690">Note that null values do not take up space in the search index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-690">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="2fa7a-691">Before you can upload documents, you must have already created the index on the service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-691">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="2fa7a-692">See [Create Index](#CreateIndex) for details about this first step.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-692">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="2fa7a-693">Add, Update, or Delete Documents</span><span class="sxs-lookup"><span data-stu-id="2fa7a-693">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="2fa7a-694">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-694">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="2fa7a-695">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-695">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="2fa7a-696">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-696">**Request**</span></span>

<span data-ttu-id="2fa7a-697">HTTPS is required for all service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-697">HTTPS is required for all service requests.</span></span> <span data-ttu-id="2fa7a-698">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-698">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="2fa7a-699">The request URI includes [index name], specifying which index to post documents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-699">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="2fa7a-700">You can only post documents to one index at a time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-700">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="2fa7a-701">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-701">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-702">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-702">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-703">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-703">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-704">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-704">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-705">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-705">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-706">`Content-Type`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-706">`Content-Type`: Required.</span></span> <span data-ttu-id="2fa7a-707">Set this to `application/json`</span><span class="sxs-lookup"><span data-stu-id="2fa7a-707">Set this to `application/json`</span></span>
* <span data-ttu-id="2fa7a-708">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-708">`api-key`: Required.</span></span> <span data-ttu-id="2fa7a-709">The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-709">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-710">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-710">It is a string value, unique to your service.</span></span> <span data-ttu-id="2fa7a-711">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-711">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="2fa7a-712">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-712">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-713">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-713">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-714">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-714">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-715">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-715">**Request Body**</span></span>

<span data-ttu-id="2fa7a-716">The body of the request contains one or more documents to be indexed.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-716">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="2fa7a-717">Documents are identified by a unique key.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-717">Documents are identified by a unique key.</span></span> <span data-ttu-id="2fa7a-718">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-718">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="2fa7a-719">Upload requests must include the document data as a set of key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-719">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="2fa7a-720">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span><span class="sxs-lookup"><span data-stu-id="2fa7a-720">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="2fa7a-721">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-721">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="2fa7a-722">**Document Actions**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-722">**Document Actions**</span></span>

* <span data-ttu-id="2fa7a-723">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-723">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="2fa7a-724">Note that all fields are replaced in the update case.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-724">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="2fa7a-725">`merge`: Merge updates an existing document with the specified fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-725">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="2fa7a-726">If the document doesn't exist, the merge will fail.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-726">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="2fa7a-727">Any field you specify in a merge will replace the existing field in the document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-727">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="2fa7a-728">This includes fields of type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-728">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="2fa7a-729">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-729">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="2fa7a-730">It will **not** be `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-730">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="2fa7a-731">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-731">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="2fa7a-732">If the document does not exist it behaves like `upload` with a new document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-732">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="2fa7a-733">`delete`: Delete removes the specified document from the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-733">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="2fa7a-734">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-734">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="2fa7a-735">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-735">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="2fa7a-736">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-736">**Response**</span></span>

<span data-ttu-id="2fa7a-737">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-737">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="2fa7a-738">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span><span class="sxs-lookup"><span data-stu-id="2fa7a-738">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="2fa7a-739">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-739">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="2fa7a-740">Items that have not been indexed have the `status` field set to false.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-740">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="2fa7a-741">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-741">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="2fa7a-742">The following table explains the various per-document status codes that can be returned in the response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-742">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="2fa7a-743">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-743">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="2fa7a-744">The latter you should retry after a delay.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-744">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="2fa7a-745">Status code</span><span class="sxs-lookup"><span data-stu-id="2fa7a-745">Status code</span></span></th>
        <th><span data-ttu-id="2fa7a-746">Meaning</span><span class="sxs-lookup"><span data-stu-id="2fa7a-746">Meaning</span></span></th>
        <th><span data-ttu-id="2fa7a-747">Retryable</span><span class="sxs-lookup"><span data-stu-id="2fa7a-747">Retryable</span></span></th>
        <th><span data-ttu-id="2fa7a-748">Notes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-748">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-749">200</span><span class="sxs-lookup"><span data-stu-id="2fa7a-749">200</span></span></td>
        <td><span data-ttu-id="2fa7a-750">Document was successfully modified or deleted.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-750">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="2fa7a-751">n/a</span><span class="sxs-lookup"><span data-stu-id="2fa7a-751">n/a</span></span></td>
        <td><span data-ttu-id="2fa7a-752">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-752">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="2fa7a-753">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-753">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-754">201</span><span class="sxs-lookup"><span data-stu-id="2fa7a-754">201</span></span></td>
        <td><span data-ttu-id="2fa7a-755">Document was successfully created.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-755">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="2fa7a-756">n/a</span><span class="sxs-lookup"><span data-stu-id="2fa7a-756">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-757">400</span><span class="sxs-lookup"><span data-stu-id="2fa7a-757">400</span></span></td>
        <td><span data-ttu-id="2fa7a-758">There was an error in the document that prevented it from being indexed.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-758">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="2fa7a-759">No</span><span class="sxs-lookup"><span data-stu-id="2fa7a-759">No</span></span></td>
        <td><span data-ttu-id="2fa7a-760">The error message in the response will indicate what is wrong with the document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-760">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-761">404</span><span class="sxs-lookup"><span data-stu-id="2fa7a-761">404</span></span></td>
        <td><span data-ttu-id="2fa7a-762">The document could not be merged because the given key doesn't exist in the index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-762">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="2fa7a-763">No</span><span class="sxs-lookup"><span data-stu-id="2fa7a-763">No</span></span></td>
        <td><span data-ttu-id="2fa7a-764">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-764">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-765">409</span><span class="sxs-lookup"><span data-stu-id="2fa7a-765">409</span></span></td>
        <td><span data-ttu-id="2fa7a-766">A version conflict was detected when attempting to index a document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-766">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="2fa7a-767">Yes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-767">Yes</span></span></td>
        <td><span data-ttu-id="2fa7a-768">This can happen when you're trying to index the same document more than once concurrently.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-768">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-769">422</span><span class="sxs-lookup"><span data-stu-id="2fa7a-769">422</span></span></td>
        <td><span data-ttu-id="2fa7a-770">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-770">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="2fa7a-771">Yes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-771">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2fa7a-772">503</span><span class="sxs-lookup"><span data-stu-id="2fa7a-772">503</span></span></td>
        <td><span data-ttu-id="2fa7a-773">Your search service is temporarily unavailable, possibly due to heavy load.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-773">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="2fa7a-774">Yes</span><span class="sxs-lookup"><span data-stu-id="2fa7a-774">Yes</span></span></td>
        <td><span data-ttu-id="2fa7a-775">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-775">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="2fa7a-776">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-776">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="2fa7a-777">You can confirm this by checking the `statusCode` property for 503.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-777">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="2fa7a-778">If this is the case, we recommend ***throttling indexing requests***.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-778">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="2fa7a-779">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-779">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="2fa7a-780">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-780">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="2fa7a-781">You must either create a new index or upgrade for higher capacity limits.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-781">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="2fa7a-782">**Example:**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-782">**Example:**</span></span>

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="2fa7a-783">Search Documents</span><span class="sxs-lookup"><span data-stu-id="2fa7a-783">Search Documents</span></span>
<span data-ttu-id="2fa7a-784">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-784">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="2fa7a-785">**When to use POST instead of GET**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-785">**When to use POST instead of GET**</span></span>

<span data-ttu-id="2fa7a-786">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-786">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="2fa7a-787">This is usually enough for most applications.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-787">This is usually enough for most applications.</span></span> <span data-ttu-id="2fa7a-788">However, some applications produce very large queries or OData filter expressions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-788">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="2fa7a-789">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-789">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="2fa7a-790">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-790">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-791">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-791">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="2fa7a-792">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-792">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="2fa7a-793">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-793">**Request**</span></span>

<span data-ttu-id="2fa7a-794">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-794">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-795">The **Search** request can be constructed using the GET or POST methods.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-795">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="2fa7a-796">The request URI specifies which index to query, for all documents that match the parameters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-796">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="2fa7a-797">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-797">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="2fa7a-798">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-798">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="2fa7a-799">For **Search** operations, this includes:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-799">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="2fa7a-800">URL encoding is only recommended on the above query parameters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-800">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="2fa7a-801">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-801">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="2fa7a-802">Also, URL encoding is only necessary when calling the REST API directly using GET.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-802">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="2fa7a-803">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-803">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<a name="SearchQueryParameters"></a>
<span data-ttu-id="2fa7a-804">**Query Parameters**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-804">**Query Parameters**</span></span>

<span data-ttu-id="2fa7a-805">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-805">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="2fa7a-806">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-806">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="2fa7a-807">The syntax for some parameters is slightly different between GET and POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-807">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="2fa7a-808">These differences are noted as applicable below:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-808">These differences are noted as applicable below:</span></span>

<span data-ttu-id="2fa7a-809">`search=[string]` (optional) - The text to search for.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-809">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="2fa7a-810">All `searchable` fields are searched by default unless `searchFields` is specified.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-810">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="2fa7a-811">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-811">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="2fa7a-812">To match any term, use `*` (this can be useful for boolean filter queries).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-812">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="2fa7a-813">Omitting this parameter has the same effect as setting it to `*`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-813">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="2fa7a-814">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-814">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="2fa7a-815">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-815">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="2fa7a-816">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-816">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="2fa7a-817">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-817">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="2fa7a-818">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-818">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="2fa7a-819">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-819">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="2fa7a-820">Target fields must be marked as `searchable`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-820">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="2fa7a-821">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, \* and "".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-821">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, \* and "".</span></span> <span data-ttu-id="2fa7a-822">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-822">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="2fa7a-823">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-823">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="2fa7a-824">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-824">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="2fa7a-825">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-825">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="2fa7a-826">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-826">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-827">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-827">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="2fa7a-828">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-828">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="2fa7a-829">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-829">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="2fa7a-830">Those terms are then used to make the request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-830">Those terms are then used to make the request.</span></span> <span data-ttu-id="2fa7a-831">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-831">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="2fa7a-832">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-832">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="2fa7a-833">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-833">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-834">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-834">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-835">`$top=#` (optional) - the number of search results to retrieve.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-835">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="2fa7a-836">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-836">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-837">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-837">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-838">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-838">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="2fa7a-839">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-839">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="2fa7a-840">Setting this value to `true` may have a performance impact.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-840">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="2fa7a-841">Note that the count returned is an approximation.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-841">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-842">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-842">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-843">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-843">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="2fa7a-844">Each expression can be either a field name or a call to the `geo.distance()` function.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-844">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="2fa7a-845">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-845">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="2fa7a-846">The default is ascending order.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-846">The default is ascending order.</span></span> <span data-ttu-id="2fa7a-847">Ties will be broken by the match scores of documents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-847">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="2fa7a-848">If no `$orderby` is specified, the default sort order is descending by document match score.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-848">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="2fa7a-849">There is a limit of 32 clauses for `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-849">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-850">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-850">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-851">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-851">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="2fa7a-852">If unspecified, all fields marked as retrievable in the schema are included.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-852">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="2fa7a-853">You can also explicitly request all fields by setting this parameter to `*`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-853">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-854">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-854">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-855">`facet=[string]` (zero or more) - A field to facet by.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-855">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="2fa7a-856">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-856">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="2fa7a-857">Valid parameters are:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-857">Valid parameters are:</span></span>

* <span data-ttu-id="2fa7a-858">`count` (max number of facet terms; default is 10).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-858">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="2fa7a-859">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-859">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="2fa7a-860">For example: `facet=category,count:5` gets the top five categories in facet results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-860">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="2fa7a-861">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-861">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="2fa7a-862">This is due to the way faceting queries are distributed across shards.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-862">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="2fa7a-863">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-863">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="2fa7a-864">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-864">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="2fa7a-865">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-865">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="2fa7a-866">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-866">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="2fa7a-867">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-867">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="2fa7a-868">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-868">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="2fa7a-869">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-869">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="2fa7a-870">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-870">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="2fa7a-871">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-871">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="2fa7a-872">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-872">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="2fa7a-873">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-873">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="2fa7a-874">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-874">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="2fa7a-875">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-875">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="2fa7a-876">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-876">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="2fa7a-877">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-877">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="2fa7a-878">The value specifies the UTC time offset to account for in setting time boundaries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-878">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="2fa7a-879">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-879">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="2fa7a-880">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-880">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="2fa7a-881">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-881">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="2fa7a-882">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-882">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="2fa7a-883">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-883">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="2fa7a-884">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-884">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="2fa7a-885">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-885">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span> <span data-ttu-id="2fa7a-886">See [OData Expression Syntax](#ODataExpressionSyntax) for details on the subset of the OData expression grammar that Azure Search supports.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-886">See [OData Expression Syntax](#ODataExpressionSyntax) for details on the subset of the OData expression grammar that Azure Search supports.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-887">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-887">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-888">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-888">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="2fa7a-889">Only `searchable` fields can be used for hit highlighting.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-889">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="2fa7a-890">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-890">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="2fa7a-891">Must be set with `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-891">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-892">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-892">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="2fa7a-893">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-893">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="2fa7a-894">Must be set with `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-894">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-895">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-895">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="2fa7a-896">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-896">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="2fa7a-897">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-897">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="2fa7a-898">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-898">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="2fa7a-899">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-899">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="2fa7a-900">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-900">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="2fa7a-901">If the values themselves contain single quotes, you can escape them by doubling.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-901">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="2fa7a-902">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-902">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="2fa7a-903">Note that quotes are only required for values that contain commas.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-903">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-904">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-904">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="2fa7a-905">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-905">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="2fa7a-906">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-906">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="2fa7a-907">By default, the entire index must be available or `Search` will return HTTP status code 503.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-907">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="2fa7a-908">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-908">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-909">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-909">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="2fa7a-910">However, not all matching documents are guaranteed to be present in the search results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-910">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="2fa7a-911">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-911">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="2fa7a-912">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-912">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-913">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-913">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-914">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-914">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-915">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-915">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="2fa7a-916">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-916">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-917">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-917">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-918">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-918">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-919">It is a string value, unique to your service URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-919">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="2fa7a-920">The **Search** request can specify either an admin key or query key for `api-key`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-920">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="2fa7a-921">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-921">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-922">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-922">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-923">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-923">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-924">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-924">**Request Body**</span></span>

<span data-ttu-id="2fa7a-925">For GET: None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-925">For GET: None.</span></span>

<span data-ttu-id="2fa7a-926">For POST:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-926">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="2fa7a-927">**Continuation of Partial Search Responses**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-927">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="2fa7a-928">Sometimes Azure Search can't return all the requested results in a single Search response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-928">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="2fa7a-929">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-929">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="2fa7a-930">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-930">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="2fa7a-931">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-931">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="2fa7a-932">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-932">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="2fa7a-933">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-933">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="2fa7a-934">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-934">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="2fa7a-935">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-935">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="2fa7a-936">Also note that you must use the same HTTP method as the original request in order to continue.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-936">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="2fa7a-937">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-937">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<a name="SearchResponse"></a>
<span data-ttu-id="2fa7a-938">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-938">**Response**</span></span>

<span data-ttu-id="2fa7a-939">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-939">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="2fa7a-940">**Examples:**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-940">**Examples:**</span></span>

<span data-ttu-id="2fa7a-941">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-941">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="2fa7a-942">Search the Index sorted descending by date.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-942">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="2fa7a-943">GET /indexes/hotels/docs?search=\*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-943">GET /indexes/hotels/docs?search=\*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-944">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-944">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="2fa7a-945">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-945">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="2fa7a-946">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-946">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-947">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-947">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="2fa7a-948">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span><span class="sxs-lookup"><span data-stu-id="2fa7a-948">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="2fa7a-949">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-949">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-950">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-950">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="2fa7a-951">In a faceted search, set an upper limit on unique terms returned in a query.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-951">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="2fa7a-952">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-952">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="2fa7a-953">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-953">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-954">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-954">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="2fa7a-955">Search the Index within specific fields; For example, a language-specific field:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-955">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="2fa7a-956">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-956">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-957">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-957">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="2fa7a-958">Search the Index across multiple fields.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-958">Search the Index across multiple fields.</span></span> <span data-ttu-id="2fa7a-959">For example, you can store and query searchable fields in multiple languages, all within the same index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-959">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="2fa7a-960">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-960">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="2fa7a-961">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-961">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-962">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-962">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="2fa7a-963">Note that you can only query one index at a time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-963">Note that you can only query one index at a time.</span></span> <span data-ttu-id="2fa7a-964">Do not create multiple indexes for each language unless you plan to query one at a time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-964">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="2fa7a-965">Paging - Get the 1st page of items (page size is 10):</span><span class="sxs-lookup"><span data-stu-id="2fa7a-965">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="2fa7a-966">GET /indexes/hotels/docs?search=\*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-966">GET /indexes/hotels/docs?search=\*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-967">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-967">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="2fa7a-968">Paging - Get the 2nd page of items (page size is 10):</span><span class="sxs-lookup"><span data-stu-id="2fa7a-968">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="2fa7a-969">GET /indexes/hotels/docs?search=\*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-969">GET /indexes/hotels/docs?search=\*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-970">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-970">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="2fa7a-971">Retrieve a specific set of fields:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-971">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="2fa7a-972">GET /indexes/hotels/docs?search=\*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-972">GET /indexes/hotels/docs?search=\*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-973">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-973">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "\*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="2fa7a-974">Retrieve documents matching a specific filter expression:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-974">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="2fa7a-975">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-975">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-976">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-976">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="2fa7a-977">Search the index and return fragments with hit highlights</span><span class="sxs-lookup"><span data-stu-id="2fa7a-977">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="2fa7a-978">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-978">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-979">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-979">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="2fa7a-980">Search the index and return documents sorted from closer to farther away from a reference location</span><span class="sxs-lookup"><span data-stu-id="2fa7a-980">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="2fa7a-981">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-981">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-982">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-982">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="2fa7a-983">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="2fa7a-983">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="2fa7a-984">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-984">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-985">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-985">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="2fa7a-986">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-986">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="2fa7a-987">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span><span class="sxs-lookup"><span data-stu-id="2fa7a-987">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="2fa7a-988">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="2fa7a-988">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="2fa7a-989">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-989">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="2fa7a-990">Note the use of `searchMode=all` above.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-990">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="2fa7a-991">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-991">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="2fa7a-992">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-992">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="2fa7a-993">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-993">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="2fa7a-994">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span><span class="sxs-lookup"><span data-stu-id="2fa7a-994">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="2fa7a-995">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span><span class="sxs-lookup"><span data-stu-id="2fa7a-995">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="2fa7a-996">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="2fa7a-996">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="2fa7a-997">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="2fa7a-997">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="2fa7a-998">Lookup Document</span><span class="sxs-lookup"><span data-stu-id="2fa7a-998">Lookup Document</span></span>
<span data-ttu-id="2fa7a-999">The **Lookup Document** operation retrieves a document from Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-999">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="2fa7a-1000">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1000">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="2fa7a-1001">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1001">**Request**</span></span>

<span data-ttu-id="2fa7a-1002">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1002">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-1003">The **Lookup Document** request can be constructed as follows.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1003">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="2fa7a-1004">Alternatively, you can use the traditional OData syntax for key lookup:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1004">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="2fa7a-1005">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1005">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="2fa7a-1006">You can only get one document at a time.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1006">You can only get one document at a time.</span></span> <span data-ttu-id="2fa7a-1007">Use **Search** to get multiple documents in a single request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1007">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="2fa7a-1008">**Query Parameters**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1008">**Query Parameters**</span></span>

<span data-ttu-id="2fa7a-1009">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1009">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="2fa7a-1010">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1010">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="2fa7a-1011">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1011">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-1012">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1012">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-1013">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1013">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-1014">Note: For this operation, the `api-version` is specified as a query parameter.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1014">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="2fa7a-1015">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1015">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-1016">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1016">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-1017">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1017">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-1018">It is a string value, unique to your service URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1018">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="2fa7a-1019">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1019">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="2fa7a-1020">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1020">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-1021">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1021">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-1022">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1022">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-1023">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1023">**Request Body**</span></span>

<span data-ttu-id="2fa7a-1024">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1024">None.</span></span>

<span data-ttu-id="2fa7a-1025">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1025">**Response**</span></span>

<span data-ttu-id="2fa7a-1026">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1026">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="2fa7a-1027">**Example**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1027">**Example**</span></span>

<span data-ttu-id="2fa7a-1028">Lookup the document that has key '2'</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1028">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="2fa7a-1029">Lookup the document that has key '3' using OData syntax:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1029">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="2fa7a-1030">Count Documents</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1030">Count Documents</span></span>
<span data-ttu-id="2fa7a-1031">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1031">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="2fa7a-1032">The `$count` syntax is part of the OData protocol.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1032">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="2fa7a-1033">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1033">**Request**</span></span>

<span data-ttu-id="2fa7a-1034">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1034">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-1035">The **Count Documents** request can be constructed using the GET method.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1035">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="2fa7a-1036">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1036">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="2fa7a-1037">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1037">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-1038">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1038">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-1039">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1039">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-1040">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1040">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-1041">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1041">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="2fa7a-1042">`Accept`: This value must be set to `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1042">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="2fa7a-1043">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1043">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-1044">It is a string value, unique to your service URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1044">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="2fa7a-1045">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1045">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="2fa7a-1046">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1046">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-1047">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1047">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-1048">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1048">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-1049">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1049">**Request Body**</span></span>

<span data-ttu-id="2fa7a-1050">None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1050">None.</span></span>

<span data-ttu-id="2fa7a-1051">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1051">**Response**</span></span>

<span data-ttu-id="2fa7a-1052">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1052">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="2fa7a-1053">The response body contains the count value as an integer formatted in plain text.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1053">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="2fa7a-1054">Suggestions</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1054">Suggestions</span></span>
<span data-ttu-id="2fa7a-1055">The **Suggestions** operation retrieves suggestions based on partial search input.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1055">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="2fa7a-1056">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1056">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="2fa7a-1057">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1057">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="2fa7a-1058">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1058">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="2fa7a-1059">A **Suggestions** operation is issued as a GET or POST request.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1059">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="2fa7a-1060">**When to use POST instead of GET**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1060">**When to use POST instead of GET**</span></span>

<span data-ttu-id="2fa7a-1061">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1061">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="2fa7a-1062">This is usually enough for most applications.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1062">This is usually enough for most applications.</span></span> <span data-ttu-id="2fa7a-1063">However, some applications produce very large queries, specifically OData filter expressions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1063">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="2fa7a-1064">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1064">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="2fa7a-1065">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1065">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1066">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1066">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="2fa7a-1067">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1067">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1068">**Request**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1068">**Request**</span></span>

<span data-ttu-id="2fa7a-1069">HTTPS is required for service requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1069">HTTPS is required for service requests.</span></span> <span data-ttu-id="2fa7a-1070">The **Suggestions** request can be constructed using the GET or POST methods.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1070">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="2fa7a-1071">The request URI specifies the name of the index to query.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1071">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="2fa7a-1072">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1072">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="2fa7a-1073">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1073">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="2fa7a-1074">For **Suggestions** operations, this includes:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1074">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="2fa7a-1075">URL encoding is only recommended on the above query parameters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1075">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="2fa7a-1076">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1076">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="2fa7a-1077">Also, URL encoding is only necessary when calling the REST API directly using GET.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1077">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="2fa7a-1078">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1078">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="2fa7a-1079">**Query Parameters**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1079">**Query Parameters**</span></span>

<span data-ttu-id="2fa7a-1080">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1080">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="2fa7a-1081">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1081">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="2fa7a-1082">The syntax for some parameters is slightly different between GET and POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1082">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="2fa7a-1083">These differences are noted as applicable below:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1083">These differences are noted as applicable below:</span></span>

<span data-ttu-id="2fa7a-1084">`search=[string]` - the search text to use to suggest queries.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1084">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="2fa7a-1085">Must be at least 1 character, and no more than 100 characters.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1085">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="2fa7a-1086">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1086">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="2fa7a-1087">Must be set with `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1087">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1088">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1088">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="2fa7a-1089">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1089">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="2fa7a-1090">Must be set with `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1090">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1091">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1091">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="2fa7a-1092">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1092">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="2fa7a-1093">A `suggester` determines which fields are scanned for suggested query terms.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1093">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="2fa7a-1094">See [Suggesters](#Suggesters) for details.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1094">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="2fa7a-1095">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1095">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="2fa7a-1096">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1096">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="2fa7a-1097">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1097">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="2fa7a-1098">Target fields must be enabled for suggestions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1098">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="2fa7a-1099">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1099">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="2fa7a-1100">Must be a number between 1 and 100.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1100">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1101">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1101">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1102">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1102">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1103">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1103">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1104">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1104">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="2fa7a-1105">Each expression can be either a field name or a call to the `geo.distance()` function.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1105">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="2fa7a-1106">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1106">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="2fa7a-1107">The default is ascending order.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1107">The default is ascending order.</span></span> <span data-ttu-id="2fa7a-1108">There is a limit of 32 clauses for `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1108">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1109">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1109">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1110">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1110">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="2fa7a-1111">If unspecified, only the document key and suggestion text is returned.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1111">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="2fa7a-1112">You can explicitly request all fields by setting this parameter to `*`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1112">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1113">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1113">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1114">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1114">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="2fa7a-1115">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1115">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="2fa7a-1116">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1116">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="2fa7a-1117">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1117">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="2fa7a-1118">However, not all matching suggestions are guaranteed to be present in the results.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1118">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="2fa7a-1119">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1119">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="2fa7a-1120">`api-version=[string]` (required).</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1120">`api-version=[string]` (required).</span></span> <span data-ttu-id="2fa7a-1121">The preview version is `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1121">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="2fa7a-1122">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1122">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="2fa7a-1123">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1123">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="2fa7a-1124">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1124">**Request Headers**</span></span>

<span data-ttu-id="2fa7a-1125">The following list describes the required and optional request headers</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1125">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="2fa7a-1126">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1126">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="2fa7a-1127">It is a string value, unique to your service URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1127">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="2fa7a-1128">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1128">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="2fa7a-1129">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1129">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="2fa7a-1130">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1130">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="2fa7a-1131">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1131">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="2fa7a-1132">**Request Body**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1132">**Request Body**</span></span>

<span data-ttu-id="2fa7a-1133">For GET: None.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1133">For GET: None.</span></span>

<span data-ttu-id="2fa7a-1134">For POST:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1134">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="2fa7a-1135">**Response**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1135">**Response**</span></span>

<span data-ttu-id="2fa7a-1136">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1136">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="2fa7a-1137">If the projection option is used to retrieve fields they are included in each element of the array:</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1137">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="2fa7a-1138">**Example**</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1138">**Example**</span></span>

<span data-ttu-id="2fa7a-1139">Retrieve 5 suggestions where the partial search input is 'lux'</span><span class="sxs-lookup"><span data-stu-id="2fa7a-1139">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
