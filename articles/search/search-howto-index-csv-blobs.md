---
title: Indexing CSV blobs with Azure Search blob indexer | Microsoft Docs
description: Learn how to index CSV blobs with Azure Search
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: af9da85c37211d2436c23cc05400031c661ef51e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555253"
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a><span data-ttu-id="97b1f-103">Indexing CSV blobs with Azure Search blob indexer</span><span class="sxs-lookup"><span data-stu-id="97b1f-103">Indexing CSV blobs with Azure Search blob indexer</span></span>
<span data-ttu-id="97b1f-104">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses delimited text blobs as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="97b1f-104">By default, [Azure Search blob indexer](search-howto-indexing-azure-blob-storage.md) parses delimited text blobs as a single chunk of text.</span></span> <span data-ttu-id="97b1f-105">However, with blobs containing CSV data, you often want to treat each line in the blob as a separate document.</span><span class="sxs-lookup"><span data-stu-id="97b1f-105">However, with blobs containing CSV data, you often want to treat each line in the blob as a separate document.</span></span> <span data-ttu-id="97b1f-106">For example, given the following delimited text:</span><span class="sxs-lookup"><span data-stu-id="97b1f-106">For example, given the following delimited text:</span></span> 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

<span data-ttu-id="97b1f-107">you might want to parse it into 2 documents, each containing "id", "datePublished", and "tags" fields.</span><span class="sxs-lookup"><span data-stu-id="97b1f-107">you might want to parse it into 2 documents, each containing "id", "datePublished", and "tags" fields.</span></span>

<span data-ttu-id="97b1f-108">In this article you will learn how to parse CSV blobs with an Azure Search blob indexer.</span><span class="sxs-lookup"><span data-stu-id="97b1f-108">In this article you will learn how to parse CSV blobs with an Azure Search blob indexer.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="97b1f-109">This functionality is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="97b1f-109">This functionality is currently in preview.</span></span> <span data-ttu-id="97b1f-110">It is available only in the REST API using version **2015-02-28-Preview**.</span><span class="sxs-lookup"><span data-stu-id="97b1f-110">It is available only in the REST API using version **2015-02-28-Preview**.</span></span> <span data-ttu-id="97b1f-111">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="97b1f-111">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span> 
> 
> 

## <a name="setting-up-csv-indexing"></a><span data-ttu-id="97b1f-112">Setting up CSV indexing</span><span class="sxs-lookup"><span data-stu-id="97b1f-112">Setting up CSV indexing</span></span>
<span data-ttu-id="97b1f-113">To index CSV blobs, create or update an indexer definition with the `delimitedText` parsing mode:</span><span class="sxs-lookup"><span data-stu-id="97b1f-113">To index CSV blobs, create or update an indexer definition with the `delimitedText` parsing mode:</span></span>  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

<span data-ttu-id="97b1f-114">For more details on the Create Indexer API, check out [Create Indexer](search-api-indexers-2015-02-28-preview.md#create-indexer).</span><span class="sxs-lookup"><span data-stu-id="97b1f-114">For more details on the Create Indexer API, check out [Create Indexer](search-api-indexers-2015-02-28-preview.md#create-indexer).</span></span>

<span data-ttu-id="97b1f-115">`firstLineContainsHeaders` indicates that the first (non-blank) line of each blob contains headers.</span><span class="sxs-lookup"><span data-stu-id="97b1f-115">`firstLineContainsHeaders` indicates that the first (non-blank) line of each blob contains headers.</span></span>
<span data-ttu-id="97b1f-116">If blobs don't contain an initial header line, the headers should be specified in the indexer configuration:</span><span class="sxs-lookup"><span data-stu-id="97b1f-116">If blobs don't contain an initial header line, the headers should be specified in the indexer configuration:</span></span> 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

<span data-ttu-id="97b1f-117">Currently, only the UTF-8 encoding is supported.</span><span class="sxs-lookup"><span data-stu-id="97b1f-117">Currently, only the UTF-8 encoding is supported.</span></span> <span data-ttu-id="97b1f-118">Also, only the comma `','` character is supported as the delimiter.</span><span class="sxs-lookup"><span data-stu-id="97b1f-118">Also, only the comma `','` character is supported as the delimiter.</span></span> <span data-ttu-id="97b1f-119">If you need support for other encodings or delimiters, please let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="97b1f-119">If you need support for other encodings or delimiters, please let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97b1f-120">When you use the delimited text parsing mode, Azure Search assumes that all blobs in your data source will be CSV.</span><span class="sxs-lookup"><span data-stu-id="97b1f-120">When you use the delimited text parsing mode, Azure Search assumes that all blobs in your data source will be CSV.</span></span> <span data-ttu-id="97b1f-121">If you need to support a mix of CSV and non-CSV blobs in the same data source, please let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="97b1f-121">If you need to support a mix of CSV and non-CSV blobs in the same data source, please let us know on [our UserVoice site](https://feedback.azure.com/forums/263029-azure-search).</span></span>
> 
> 

## <a name="request-examples"></a><span data-ttu-id="97b1f-122">Request examples</span><span class="sxs-lookup"><span data-stu-id="97b1f-122">Request examples</span></span>
<span data-ttu-id="97b1f-123">Putting this all together, here are the complete payload examples.</span><span class="sxs-lookup"><span data-stu-id="97b1f-123">Putting this all together, here are the complete payload examples.</span></span> 

<span data-ttu-id="97b1f-124">Datasource:</span><span class="sxs-lookup"><span data-stu-id="97b1f-124">Datasource:</span></span> 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

<span data-ttu-id="97b1f-125">Indexer:</span><span class="sxs-lookup"><span data-stu-id="97b1f-125">Indexer:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="97b1f-126">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="97b1f-126">Help us make Azure Search better</span></span>
<span data-ttu-id="97b1f-127">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="97b1f-127">If you have feature requests or ideas for improvements, please reach out to us on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

