---
title: Indexing JSON blobs with Azure Search blob indexer
description: Indexing JSON blobs with Azure Search blob indexer
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: c4a9e57cda4ba5b4db742c1a37686a802f58212f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550883"
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a><span data-ttu-id="7c2d6-103">Indexing JSON blobs with Azure Search blob indexer</span><span class="sxs-lookup"><span data-stu-id="7c2d6-103">Indexing JSON blobs with Azure Search blob indexer</span></span>
<span data-ttu-id="7c2d6-104">This article shows how to configure Azure Search blob indexer to extract structured content from blobs that contain JSON.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-104">This article shows how to configure Azure Search blob indexer to extract structured content from blobs that contain JSON.</span></span>

## <a name="scenarios"></a><span data-ttu-id="7c2d6-105">Scenarios</span><span class="sxs-lookup"><span data-stu-id="7c2d6-105">Scenarios</span></span>
<span data-ttu-id="7c2d6-106">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses JSON blobs as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-106">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses JSON blobs as a single chunk of text.</span></span> <span data-ttu-id="7c2d6-107">Often, you want to preserve the structure of your JSON documents.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-107">Often, you want to preserve the structure of your JSON documents.</span></span> <span data-ttu-id="7c2d6-108">For example, given the JSON document</span><span class="sxs-lookup"><span data-stu-id="7c2d6-108">For example, given the JSON document</span></span>

    {
        "article" : {
             "text" : "A hopefully useful article explaining how to parse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

<span data-ttu-id="7c2d6-109">you might want to parse it into an Azure Search document with "text", "datePublished", and "tags" fields.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-109">you might want to parse it into an Azure Search document with "text", "datePublished", and "tags" fields.</span></span>

<span data-ttu-id="7c2d6-110">Alternatively, when your blobs contain an **array of JSON objects**, you may want each element of the array to become a separate Azure Search document.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-110">Alternatively, when your blobs contain an **array of JSON objects**, you may want each element of the array to become a separate Azure Search document.</span></span> <span data-ttu-id="7c2d6-111">For example, given a blob with this JSON:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-111">For example, given a blob with this JSON:</span></span>  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

<span data-ttu-id="7c2d6-112">you can populate your Azure Search index with three separate documents, each with "id" and "text" fields.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-112">you can populate your Azure Search index with three separate documents, each with "id" and "text" fields.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c2d6-113">The JSON array parsing functionality is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-113">The JSON array parsing functionality is currently in preview.</span></span> <span data-ttu-id="7c2d6-114">It is available only in the REST API using version **2015-02-28-Preview**.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-114">It is available only in the REST API using version **2015-02-28-Preview**.</span></span> <span data-ttu-id="7c2d6-115">Remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-115">Remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
>
>

## <a name="setting-up-json-indexing"></a><span data-ttu-id="7c2d6-116">Setting up JSON indexing</span><span class="sxs-lookup"><span data-stu-id="7c2d6-116">Setting up JSON indexing</span></span>
<span data-ttu-id="7c2d6-117">Indexing JSON blobs is similar to the regular document extraction.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-117">Indexing JSON blobs is similar to the regular document extraction.</span></span> <span data-ttu-id="7c2d6-118">First, create the datasource exactly as you would normally:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-118">First, create the datasource exactly as you would normally:</span></span> 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

<span data-ttu-id="7c2d6-119">Then create the target search index if you don't already have one.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-119">Then create the target search index if you don't already have one.</span></span> 

<span data-ttu-id="7c2d6-120">Finally create an indexer and set the `parsingMode` parameter to `json` (to index each blob as a single document) or `jsonArray` (if your blobs contain JSON arrays, and you need each element of an array to be treated as a separate document):</span><span class="sxs-lookup"><span data-stu-id="7c2d6-120">Finally create an indexer and set the `parsingMode` parameter to `json` (to index each blob as a single document) or `jsonArray` (if your blobs contain JSON arrays, and you need each element of an array to be treated as a separate document):</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

<span data-ttu-id="7c2d6-121">If needed, use **field mappings** to pick the properties of the source JSON document used to populate your target search index, as shown in the next section.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-121">If needed, use **field mappings** to pick the properties of the source JSON document used to populate your target search index, as shown in the next section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c2d6-122">When you use `json` or `jsonArray` parsing mode, Azure Search assumes that all blobs in your data source contain JSON.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-122">When you use `json` or `jsonArray` parsing mode, Azure Search assumes that all blobs in your data source contain JSON.</span></span> <span data-ttu-id="7c2d6-123">If you need to support a mix of JSON and non-JSON blobs in the same data source, let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="7c2d6-123">If you need to support a mix of JSON and non-JSON blobs in the same data source, let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span></span>
>
>

## <a name="using-field-mappings-to-build-search-documents"></a><span data-ttu-id="7c2d6-124">Using field mappings to build search documents</span><span class="sxs-lookup"><span data-stu-id="7c2d6-124">Using field mappings to build search documents</span></span>
<span data-ttu-id="7c2d6-125">Currently, Azure Search cannot index arbitrary JSON documents directly, because it supports only primitive data types, string arrays, and GeoJSON points.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-125">Currently, Azure Search cannot index arbitrary JSON documents directly, because it supports only primitive data types, string arrays, and GeoJSON points.</span></span> <span data-ttu-id="7c2d6-126">However, you can use **field mappings** to pick parts of your JSON document and "lift" them into top-level fields of the search document.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-126">However, you can use **field mappings** to pick parts of your JSON document and "lift" them into top-level fields of the search document.</span></span> <span data-ttu-id="7c2d6-127">To learn about field mappings basics, see [Azure Search indexer field mappings bridge the differences between data sources and search indexes](search-indexer-field-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="7c2d6-127">To learn about field mappings basics, see [Azure Search indexer field mappings bridge the differences between data sources and search indexes](search-indexer-field-mappings.md).</span></span>

<span data-ttu-id="7c2d6-128">Coming back to our example JSON document:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-128">Coming back to our example JSON document:</span></span>

    {
        "article" : {
             "text" : "A hopefully useful article explaining how to parse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

<span data-ttu-id="7c2d6-129">Let's say you have a search index with the following fields: `text` of type `Edm.String`, `date` of type `Edm.DateTimeOffset`, and `tags` of type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-129">Let's say you have a search index with the following fields: `text` of type `Edm.String`, `date` of type `Edm.DateTimeOffset`, and `tags` of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="7c2d6-130">To map your JSON into the desired shape, use the following field mappings:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-130">To map your JSON into the desired shape, use the following field mappings:</span></span>

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

<span data-ttu-id="7c2d6-131">The source field names in the mappings are specified using the [JSON Pointer](http://tools.ietf.org/html/rfc6901) notation.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-131">The source field names in the mappings are specified using the [JSON Pointer](http://tools.ietf.org/html/rfc6901) notation.</span></span> <span data-ttu-id="7c2d6-132">You start with a forward slash to refer to the root of your JSON document, then pick the desired property (at arbitrary level of nesting) by using forward slash-separated path.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-132">You start with a forward slash to refer to the root of your JSON document, then pick the desired property (at arbitrary level of nesting) by using forward slash-separated path.</span></span>

<span data-ttu-id="7c2d6-133">You can also refer to individual array elements by using a zero-based index.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-133">You can also refer to individual array elements by using a zero-based index.</span></span> <span data-ttu-id="7c2d6-134">For example, to pick the first element of the "tags" array from the above example, use a field mapping like this:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-134">For example, to pick the first element of the "tags" array from the above example, use a field mapping like this:</span></span>

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> <span data-ttu-id="7c2d6-135">If a source field name in a field mapping path refers to a property that doesn't exist in JSON, that mapping is skipped without an error.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-135">If a source field name in a field mapping path refers to a property that doesn't exist in JSON, that mapping is skipped without an error.</span></span> <span data-ttu-id="7c2d6-136">This is done so that we can support documents with a different schema (which is a common use case).</span><span class="sxs-lookup"><span data-stu-id="7c2d6-136">This is done so that we can support documents with a different schema (which is a common use case).</span></span> <span data-ttu-id="7c2d6-137">Because there is no validation, you need to take care to avoid typos in your field mapping specification.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-137">Because there is no validation, you need to take care to avoid typos in your field mapping specification.</span></span>
>
>

<span data-ttu-id="7c2d6-138">If your JSON documents only contain simple top-level properties, you may not need field mappings at all.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-138">If your JSON documents only contain simple top-level properties, you may not need field mappings at all.</span></span> <span data-ttu-id="7c2d6-139">For example, if your JSON looks like this, the top-level properties "text", "datePublished" and "tags" directly maps to the corresponding fields in the search index:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-139">For example, if your JSON looks like this, the top-level properties "text", "datePublished" and "tags" directly maps to the corresponding fields in the search index:</span></span>

    {
       "text" : "A hopefully useful article explaining how to parse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

<span data-ttu-id="7c2d6-140">Here's a complete indexer payload with field mappings:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-140">Here's a complete indexer payload with field mappings:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
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

## <a name="indexing-nested-json-arrays"></a><span data-ttu-id="7c2d6-141">Indexing nested JSON arrays</span><span class="sxs-lookup"><span data-stu-id="7c2d6-141">Indexing nested JSON arrays</span></span>
<span data-ttu-id="7c2d6-142">What if you wish to index an array of JSON objects, but that array is nested somewhere within the document?</span><span class="sxs-lookup"><span data-stu-id="7c2d6-142">What if you wish to index an array of JSON objects, but that array is nested somewhere within the document?</span></span> <span data-ttu-id="7c2d6-143">You can pick which property contains the array using the `documentRoot` configuration property.</span><span class="sxs-lookup"><span data-stu-id="7c2d6-143">You can pick which property contains the array using the `documentRoot` configuration property.</span></span> <span data-ttu-id="7c2d6-144">For example, if your blobs look like this:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-144">For example, if your blobs look like this:</span></span>

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use the documentRoot property" },
                { "id" : "2", "text" : "to pluck the array you want to index" },
                { "id" : "3", "text" : "even if it's nested inside the document" }  
            ]
        }
    }

<span data-ttu-id="7c2d6-145">use this configuration to index the array contained in the `level2` property:</span><span class="sxs-lookup"><span data-stu-id="7c2d6-145">use this configuration to index the array contained in the `level2` property:</span></span>

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="7c2d6-146">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="7c2d6-146">Help us make Azure Search better</span></span>
<span data-ttu-id="7c2d6-147">If you have feature requests or ideas for improvements, reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="7c2d6-147">If you have feature requests or ideas for improvements, reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
