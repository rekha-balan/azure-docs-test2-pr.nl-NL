---
title: Indexing JSON blobs with Azure Search blob indexer
description: Indexing JSON blobs with Azure Search blob indexer
author: chaosrealm
manager: jlembicz
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: eugenesh
ms.openlocfilehash: 5b4cd1c592c4cd965a0b5d9e4fb8eef84a6bea91
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44831051"
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a><span data-ttu-id="6e41b-103">Indexing JSON blobs with Azure Search blob indexer</span><span class="sxs-lookup"><span data-stu-id="6e41b-103">Indexing JSON blobs with Azure Search blob indexer</span></span>
<span data-ttu-id="6e41b-104">This article shows you how to configure an Azure Search blob indexer to extract structured content from JSON blobs in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6e41b-104">This article shows you how to configure an Azure Search blob indexer to extract structured content from JSON blobs in Azure Blob storage.</span></span>

<span data-ttu-id="6e41b-105">JSON blobs in Azure Blob storage are typically either a single JSON document or a JSON array.</span><span class="sxs-lookup"><span data-stu-id="6e41b-105">JSON blobs in Azure Blob storage are typically either a single JSON document or a JSON array.</span></span> <span data-ttu-id="6e41b-106">The blob indexer in Azure Search can parse either construction, depending on how you set the **parsingMode** parameter on the request.</span><span class="sxs-lookup"><span data-stu-id="6e41b-106">The blob indexer in Azure Search can parse either construction, depending on how you set the **parsingMode** parameter on the request.</span></span>

| <span data-ttu-id="6e41b-107">JSON document</span><span class="sxs-lookup"><span data-stu-id="6e41b-107">JSON document</span></span> | <span data-ttu-id="6e41b-108">parsingMode</span><span class="sxs-lookup"><span data-stu-id="6e41b-108">parsingMode</span></span> | <span data-ttu-id="6e41b-109">Description</span><span class="sxs-lookup"><span data-stu-id="6e41b-109">Description</span></span> | <span data-ttu-id="6e41b-110">Availability</span><span class="sxs-lookup"><span data-stu-id="6e41b-110">Availability</span></span> |
|--------------|-------------|--------------|--------------|
| <span data-ttu-id="6e41b-111">One per blob</span><span class="sxs-lookup"><span data-stu-id="6e41b-111">One per blob</span></span> | `json` | <span data-ttu-id="6e41b-112">Parses JSON blobs as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="6e41b-112">Parses JSON blobs as a single chunk of text.</span></span> <span data-ttu-id="6e41b-113">Each JSON blob becomes a single Azure Search document.</span><span class="sxs-lookup"><span data-stu-id="6e41b-113">Each JSON blob becomes a single Azure Search document.</span></span> | <span data-ttu-id="6e41b-114">Generally available in both [REST](https://docs.microsoft.com/rest/api/searchservice/indexer-operations) and [.NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer) APIs.</span><span class="sxs-lookup"><span data-stu-id="6e41b-114">Generally available in both [REST](https://docs.microsoft.com/rest/api/searchservice/indexer-operations) and [.NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer) APIs.</span></span> |
| <span data-ttu-id="6e41b-115">Multiple per blob</span><span class="sxs-lookup"><span data-stu-id="6e41b-115">Multiple per blob</span></span> | `jsonArray` | <span data-ttu-id="6e41b-116">Parses a JSON array in the blob, where each element of the array becomes a separate Azure Search document.</span><span class="sxs-lookup"><span data-stu-id="6e41b-116">Parses a JSON array in the blob, where each element of the array becomes a separate Azure Search document.</span></span>  | <span data-ttu-id="6e41b-117">In preview, in [REST api-version=`2017-11-11-Preview`](search-api-2017-11-11-preview.md) and [.NET SDK Preview](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="6e41b-117">In preview, in [REST api-version=`2017-11-11-Preview`](search-api-2017-11-11-preview.md) and [.NET SDK Preview](https://aka.ms/search-sdk-preview).</span></span> |

> [!Note]
> <span data-ttu-id="6e41b-118">Preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="6e41b-118">Preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
>

## <a name="setting-up-json-indexing"></a><span data-ttu-id="6e41b-119">Setting up JSON indexing</span><span class="sxs-lookup"><span data-stu-id="6e41b-119">Setting up JSON indexing</span></span>
<span data-ttu-id="6e41b-120">Indexing JSON blobs is similar to the regular document extraction in a three-part workflow common to all indexers in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6e41b-120">Indexing JSON blobs is similar to the regular document extraction in a three-part workflow common to all indexers in Azure Search.</span></span>

### <a name="step-1-create-a-data-source"></a><span data-ttu-id="6e41b-121">Step 1: Create a data source</span><span class="sxs-lookup"><span data-stu-id="6e41b-121">Step 1: Create a data source</span></span>

<span data-ttu-id="6e41b-122">The first step is to provide data source connection information used by the indexer.</span><span class="sxs-lookup"><span data-stu-id="6e41b-122">The first step is to provide data source connection information used by the indexer.</span></span> <span data-ttu-id="6e41b-123">The data source type, specified here as `azureblob`, determines which data extraction behaviors are invoked by the indexer.</span><span class="sxs-lookup"><span data-stu-id="6e41b-123">The data source type, specified here as `azureblob`, determines which data extraction behaviors are invoked by the indexer.</span></span> <span data-ttu-id="6e41b-124">For JSON blob indexing, data source definition is the same for both JSON documents and arrays.</span><span class="sxs-lookup"><span data-stu-id="6e41b-124">For JSON blob indexing, data source definition is the same for both JSON documents and arrays.</span></span> 

    POST https://[service name].search.windows.net/datasources?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

### <a name="step-2-create-a-target-search-index"></a><span data-ttu-id="6e41b-125">Step 2: Create a target search index</span><span class="sxs-lookup"><span data-stu-id="6e41b-125">Step 2: Create a target search index</span></span> 

<span data-ttu-id="6e41b-126">Indexers are paired with an index schema.</span><span class="sxs-lookup"><span data-stu-id="6e41b-126">Indexers are paired with an index schema.</span></span> <span data-ttu-id="6e41b-127">If you are using the API (rather than the portal), prepare an index in advance so that you can specify it on the indexer operation.</span><span class="sxs-lookup"><span data-stu-id="6e41b-127">If you are using the API (rather than the portal), prepare an index in advance so that you can specify it on the indexer operation.</span></span> 

> [!Note]
> <span data-ttu-id="6e41b-128">Indexers are exposed in the portal through the **Import** action for a limited number of generally available indexers.</span><span class="sxs-lookup"><span data-stu-id="6e41b-128">Indexers are exposed in the portal through the **Import** action for a limited number of generally available indexers.</span></span> <span data-ttu-id="6e41b-129">Often, the import workflow can often construct a preliminary index based on metadata in the source.</span><span class="sxs-lookup"><span data-stu-id="6e41b-129">Often, the import workflow can often construct a preliminary index based on metadata in the source.</span></span> <span data-ttu-id="6e41b-130">For more information, see [Import data into Azure Search in the portal](search-import-data-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6e41b-130">For more information, see [Import data into Azure Search in the portal](search-import-data-portal.md).</span></span>

### <a name="step-3-configure-and-run-the-indexer"></a><span data-ttu-id="6e41b-131">Step 3: Configure and run the indexer</span><span class="sxs-lookup"><span data-stu-id="6e41b-131">Step 3: Configure and run the indexer</span></span>

<span data-ttu-id="6e41b-132">Until now, definitions for the data source and index have been parsingMode agnostic.</span><span class="sxs-lookup"><span data-stu-id="6e41b-132">Until now, definitions for the data source and index have been parsingMode agnostic.</span></span> <span data-ttu-id="6e41b-133">However, in step 3 for Indexer configuration, the path diverges depending on how you want the JSON blob content to be parsed and structured in an Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="6e41b-133">However, in step 3 for Indexer configuration, the path diverges depending on how you want the JSON blob content to be parsed and structured in an Azure Search index.</span></span>

<span data-ttu-id="6e41b-134">When calling the indexer, do the following:</span><span class="sxs-lookup"><span data-stu-id="6e41b-134">When calling the indexer, do the following:</span></span>

+ <span data-ttu-id="6e41b-135">Set the **parsingMode** parameter to `json` (to index each blob as a single document) or `jsonArray` (if your blobs contain JSON arrays and you need each element of an array to be treated as a separate document).</span><span class="sxs-lookup"><span data-stu-id="6e41b-135">Set the **parsingMode** parameter to `json` (to index each blob as a single document) or `jsonArray` (if your blobs contain JSON arrays and you need each element of an array to be treated as a separate document).</span></span>

+ <span data-ttu-id="6e41b-136">Optionally, use **field mappings** to choose which properties of the source JSON document are used to populate your target search index.</span><span class="sxs-lookup"><span data-stu-id="6e41b-136">Optionally, use **field mappings** to choose which properties of the source JSON document are used to populate your target search index.</span></span> <span data-ttu-id="6e41b-137">For JSON arrays, if the array exists as a lower level property, you can set a document root indicating where the array is placed within the blob.</span><span class="sxs-lookup"><span data-stu-id="6e41b-137">For JSON arrays, if the array exists as a lower level property, you can set a document root indicating where the array is placed within the blob.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e41b-138">When you use `json` or `jsonArray` parsing mode, Azure Search assumes that all blobs in your data source contain JSON.</span><span class="sxs-lookup"><span data-stu-id="6e41b-138">When you use `json` or `jsonArray` parsing mode, Azure Search assumes that all blobs in your data source contain JSON.</span></span> <span data-ttu-id="6e41b-139">If you need to support a mix of JSON and non-JSON blobs in the same data source, let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="6e41b-139">If you need to support a mix of JSON and non-JSON blobs in the same data source, let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span></span>


## <a name="how-to-parse-single-json-blobs"></a><span data-ttu-id="6e41b-140">How to parse single JSON blobs</span><span class="sxs-lookup"><span data-stu-id="6e41b-140">How to parse single JSON blobs</span></span>

<span data-ttu-id="6e41b-141">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses JSON blobs as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="6e41b-141">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses JSON blobs as a single chunk of text.</span></span> <span data-ttu-id="6e41b-142">Often, you want to preserve the structure of your JSON documents.</span><span class="sxs-lookup"><span data-stu-id="6e41b-142">Often, you want to preserve the structure of your JSON documents.</span></span> <span data-ttu-id="6e41b-143">For example, assume you have the following JSON document in Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="6e41b-143">For example, assume you have the following JSON document in Azure Blob storage:</span></span>

    {
        "article" : {
            "text" : "A hopefully useful article explaining how to parse JSON blobs",
            "datePublished" : "2016-04-13",
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

### <a name="indexer-definition-for-single-json-blobs"></a><span data-ttu-id="6e41b-144">Indexer definition for single JSON blobs</span><span class="sxs-lookup"><span data-stu-id="6e41b-144">Indexer definition for single JSON blobs</span></span>

<span data-ttu-id="6e41b-145">Using the Azure Search blob indexer, a JSON document similar to the previous example is parsed into a single Azure Search document.</span><span class="sxs-lookup"><span data-stu-id="6e41b-145">Using the Azure Search blob indexer, a JSON document similar to the previous example is parsed into a single Azure Search document.</span></span> <span data-ttu-id="6e41b-146">The indexer loads an index by matching "text", "datePublished", and "tags" from the source against identically named and typed target fields.</span><span class="sxs-lookup"><span data-stu-id="6e41b-146">The indexer loads an index by matching "text", "datePublished", and "tags" from the source against identically named and typed target fields.</span></span>

<span data-ttu-id="6e41b-147">Configuration is provided in the body of an indexer operation.</span><span class="sxs-lookup"><span data-stu-id="6e41b-147">Configuration is provided in the body of an indexer operation.</span></span> <span data-ttu-id="6e41b-148">Recall that the data source object, previously defined, specifies the data source type and connection information.</span><span class="sxs-lookup"><span data-stu-id="6e41b-148">Recall that the data source object, previously defined, specifies the data source type and connection information.</span></span> <span data-ttu-id="6e41b-149">Additionally, the target index must also exist as an empty container in your service.</span><span class="sxs-lookup"><span data-stu-id="6e41b-149">Additionally, the target index must also exist as an empty container in your service.</span></span> <span data-ttu-id="6e41b-150">Schedule and parameters are optional, but if you omit them, the indexer runs immediately, using `json` as the parsing mode.</span><span class="sxs-lookup"><span data-stu-id="6e41b-150">Schedule and parameters are optional, but if you omit them, the indexer runs immediately, using `json` as the parsing mode.</span></span>

<span data-ttu-id="6e41b-151">A fully specified request might look as follows:</span><span class="sxs-lookup"><span data-stu-id="6e41b-151">A fully specified request might look as follows:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

<span data-ttu-id="6e41b-152">As noted, field mappings are not required.</span><span class="sxs-lookup"><span data-stu-id="6e41b-152">As noted, field mappings are not required.</span></span> <span data-ttu-id="6e41b-153">Given an index with "text", "datePublished, and "tags" fields, the blob indexer can infer the correct mapping without a field mapping present in the request.</span><span class="sxs-lookup"><span data-stu-id="6e41b-153">Given an index with "text", "datePublished, and "tags" fields, the blob indexer can infer the correct mapping without a field mapping present in the request.</span></span>

## <a name="how-to-parse-json-arrays-preview"></a><span data-ttu-id="6e41b-154">How to parse JSON arrays (preview)</span><span class="sxs-lookup"><span data-stu-id="6e41b-154">How to parse JSON arrays (preview)</span></span>

<span data-ttu-id="6e41b-155">Alternatively, you can opt for the JSON array preview feature.</span><span class="sxs-lookup"><span data-stu-id="6e41b-155">Alternatively, you can opt for the JSON array preview feature.</span></span> <span data-ttu-id="6e41b-156">This capability is useful when blobs contain an *array of JSON objects*, and you want each element to become a separate Azure Search document.</span><span class="sxs-lookup"><span data-stu-id="6e41b-156">This capability is useful when blobs contain an *array of JSON objects*, and you want each element to become a separate Azure Search document.</span></span> <span data-ttu-id="6e41b-157">For example, given the following JSON blob, you can populate your Azure Search index with three separate documents, each with "id" and "text" fields.</span><span class="sxs-lookup"><span data-stu-id="6e41b-157">For example, given the following JSON blob, you can populate your Azure Search index with three separate documents, each with "id" and "text" fields.</span></span>  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

### <a name="indexer-definition-for-a-json-array"></a><span data-ttu-id="6e41b-158">Indexer definition for a JSON array</span><span class="sxs-lookup"><span data-stu-id="6e41b-158">Indexer definition for a JSON array</span></span>

<span data-ttu-id="6e41b-159">For a JSON array, the indexer request uses the preview API and the `jsonArray` parser.</span><span class="sxs-lookup"><span data-stu-id="6e41b-159">For a JSON array, the indexer request uses the preview API and the `jsonArray` parser.</span></span> <span data-ttu-id="6e41b-160">These are the only two array-specific requirements for indexing JSON blobs.</span><span class="sxs-lookup"><span data-stu-id="6e41b-160">These are the only two array-specific requirements for indexing JSON blobs.</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2017-11-11-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "jsonArray" } }
    }

<span data-ttu-id="6e41b-161">Again, notice that field mappings are not required.</span><span class="sxs-lookup"><span data-stu-id="6e41b-161">Again, notice that field mappings are not required.</span></span> <span data-ttu-id="6e41b-162">Given an index with "id" and "text" fields, the blob indexer can infer the correct mapping without a field mapping list.</span><span class="sxs-lookup"><span data-stu-id="6e41b-162">Given an index with "id" and "text" fields, the blob indexer can infer the correct mapping without a field mapping list.</span></span>

<a name="nested-json-arrays"></a>

### <a name="nested-json-arrays"></a><span data-ttu-id="6e41b-163">Nested JSON arrays</span><span class="sxs-lookup"><span data-stu-id="6e41b-163">Nested JSON arrays</span></span>
<span data-ttu-id="6e41b-164">What if you wish to index an array of JSON objects, but that array is nested somewhere within the document?</span><span class="sxs-lookup"><span data-stu-id="6e41b-164">What if you wish to index an array of JSON objects, but that array is nested somewhere within the document?</span></span> <span data-ttu-id="6e41b-165">You can pick which property contains the array using the `documentRoot` configuration property.</span><span class="sxs-lookup"><span data-stu-id="6e41b-165">You can pick which property contains the array using the `documentRoot` configuration property.</span></span> <span data-ttu-id="6e41b-166">For example, if your blobs look like this:</span><span class="sxs-lookup"><span data-stu-id="6e41b-166">For example, if your blobs look like this:</span></span>

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use the documentRoot property" },
                { "id" : "2", "text" : "to pluck the array you want to index" },
                { "id" : "3", "text" : "even if it's nested inside the document" }  
            ]
        }
    }

<span data-ttu-id="6e41b-167">Use this configuration to index the array contained in the `level2` property:</span><span class="sxs-lookup"><span data-stu-id="6e41b-167">Use this configuration to index the array contained in the `level2` property:</span></span>

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="using-field-mappings-to-build-search-documents"></a><span data-ttu-id="6e41b-168">Using field mappings to build search documents</span><span class="sxs-lookup"><span data-stu-id="6e41b-168">Using field mappings to build search documents</span></span>

<span data-ttu-id="6e41b-169">When source and target fields are not perfectly aligned, you can define a field mapping section in the request body for explicit field-to-field associations.</span><span class="sxs-lookup"><span data-stu-id="6e41b-169">When source and target fields are not perfectly aligned, you can define a field mapping section in the request body for explicit field-to-field associations.</span></span>

<span data-ttu-id="6e41b-170">Currently, Azure Search cannot index arbitrary JSON documents directly, because it supports only primitive data types, string arrays, and GeoJSON points.</span><span class="sxs-lookup"><span data-stu-id="6e41b-170">Currently, Azure Search cannot index arbitrary JSON documents directly, because it supports only primitive data types, string arrays, and GeoJSON points.</span></span> <span data-ttu-id="6e41b-171">However, you can use **field mappings** to pick parts of your JSON document and "lift" them into top-level fields of the search document.</span><span class="sxs-lookup"><span data-stu-id="6e41b-171">However, you can use **field mappings** to pick parts of your JSON document and "lift" them into top-level fields of the search document.</span></span> <span data-ttu-id="6e41b-172">To learn about field mappings basics, see [Field mappings in Azure Search indexers](search-indexer-field-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="6e41b-172">To learn about field mappings basics, see [Field mappings in Azure Search indexers](search-indexer-field-mappings.md).</span></span>

<span data-ttu-id="6e41b-173">Revisiting our example JSON document:</span><span class="sxs-lookup"><span data-stu-id="6e41b-173">Revisiting our example JSON document:</span></span>

    {
        "article" : {
            "text" : "A hopefully useful article explaining how to parse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

<span data-ttu-id="6e41b-174">Assume a search index with the following fields: `text` of type `Edm.String`, `date` of type `Edm.DateTimeOffset`, and `tags` of type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="6e41b-174">Assume a search index with the following fields: `text` of type `Edm.String`, `date` of type `Edm.DateTimeOffset`, and `tags` of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="6e41b-175">Notice the discrepancy between "datePublished" in the source and `date` field in the index.</span><span class="sxs-lookup"><span data-stu-id="6e41b-175">Notice the discrepancy between "datePublished" in the source and `date` field in the index.</span></span> <span data-ttu-id="6e41b-176">To map your JSON into the desired shape, use the following field mappings:</span><span class="sxs-lookup"><span data-stu-id="6e41b-176">To map your JSON into the desired shape, use the following field mappings:</span></span>

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

<span data-ttu-id="6e41b-177">The source field names in the mappings are specified using the [JSON Pointer](http://tools.ietf.org/html/rfc6901) notation.</span><span class="sxs-lookup"><span data-stu-id="6e41b-177">The source field names in the mappings are specified using the [JSON Pointer](http://tools.ietf.org/html/rfc6901) notation.</span></span> <span data-ttu-id="6e41b-178">You start with a forward slash to refer to the root of your JSON document, then pick the desired property (at arbitrary level of nesting) by using forward slash-separated path.</span><span class="sxs-lookup"><span data-stu-id="6e41b-178">You start with a forward slash to refer to the root of your JSON document, then pick the desired property (at arbitrary level of nesting) by using forward slash-separated path.</span></span>

<span data-ttu-id="6e41b-179">You can also refer to individual array elements by using a zero-based index.</span><span class="sxs-lookup"><span data-stu-id="6e41b-179">You can also refer to individual array elements by using a zero-based index.</span></span> <span data-ttu-id="6e41b-180">For example, to pick the first element of the "tags" array from the above example, use a field mapping like this:</span><span class="sxs-lookup"><span data-stu-id="6e41b-180">For example, to pick the first element of the "tags" array from the above example, use a field mapping like this:</span></span>

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> <span data-ttu-id="6e41b-181">If a source field name in a field mapping path refers to a property that doesn't exist in JSON, that mapping is skipped without an error.</span><span class="sxs-lookup"><span data-stu-id="6e41b-181">If a source field name in a field mapping path refers to a property that doesn't exist in JSON, that mapping is skipped without an error.</span></span> <span data-ttu-id="6e41b-182">This is done so that we can support documents with a different schema (which is a common use case).</span><span class="sxs-lookup"><span data-stu-id="6e41b-182">This is done so that we can support documents with a different schema (which is a common use case).</span></span> <span data-ttu-id="6e41b-183">Because there is no validation, you need to take care to avoid typos in your field mapping specification.</span><span class="sxs-lookup"><span data-stu-id="6e41b-183">Because there is no validation, you need to take care to avoid typos in your field mapping specification.</span></span>
>
>

## <a name="example-indexer-request-with-field-mappings"></a><span data-ttu-id="6e41b-184">Example: Indexer request with field mappings</span><span class="sxs-lookup"><span data-stu-id="6e41b-184">Example: Indexer request with field mappings</span></span>

<span data-ttu-id="6e41b-185">The following example is a fully specified indexer payload, including field mappings:</span><span class="sxs-lookup"><span data-stu-id="6e41b-185">The following example is a fully specified indexer payload, including field mappings:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }


## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="6e41b-186">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="6e41b-186">Help us make Azure Search better</span></span>
<span data-ttu-id="6e41b-187">If you have feature requests or ideas for improvements, reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="6e41b-187">If you have feature requests or ideas for improvements, reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e41b-188">See also</span><span class="sxs-lookup"><span data-stu-id="6e41b-188">See also</span></span>

+ [<span data-ttu-id="6e41b-189">Indexers in Azure Search</span><span class="sxs-lookup"><span data-stu-id="6e41b-189">Indexers in Azure Search</span></span>](search-indexer-overview.md)
+ [<span data-ttu-id="6e41b-190">Indexing Azure Blob Storage with Azure Search</span><span class="sxs-lookup"><span data-stu-id="6e41b-190">Indexing Azure Blob Storage with Azure Search</span></span>](search-howto-index-json-blobs.md)
+ [<span data-ttu-id="6e41b-191">Indexing CSV blobs with Azure Search blob indexer</span><span class="sxs-lookup"><span data-stu-id="6e41b-191">Indexing CSV blobs with Azure Search blob indexer</span></span>](search-howto-index-csv-blobs.md)
+ [<span data-ttu-id="6e41b-192">Tutorial: Search semi-structured data from Azure Blob storage </span><span class="sxs-lookup"><span data-stu-id="6e41b-192">Tutorial: Search semi-structured data from Azure Blob storage </span></span>](search-semi-structured-data.md)
