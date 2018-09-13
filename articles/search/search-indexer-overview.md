---
title: Indexers in Azure Search | Microsoft Docs
description: Crawl Azure SQL database, DocumentDB, or Azure storage to extract searchable data and populate an Azure Search index.
services: search
documentationcenter: ''
author: HeidiSteen
manager: jhubbard
editor: ''
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: fd46641709d260f8b468556972aae14205fdb515
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563048"
---
# <a name="indexers-in-azure-search"></a><span data-ttu-id="b616d-103">Indexers in Azure Search</span><span class="sxs-lookup"><span data-stu-id="b616d-103">Indexers in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [Overview](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [DocumentDB](search-howto-index-documentdb.md)
> * [Blob Storage (preview)](search-howto-indexing-azure-blob-storage.md)
> * [Table Storage (preview)](search-howto-indexing-azure-tables.md)
>
>

<span data-ttu-id="b616d-110">An **indexer** in Azure Search is a crawler that extracts searchable data and metadata from an external data source and populates an index based on field-to-field mappings between the index and your data source.</span><span class="sxs-lookup"><span data-stu-id="b616d-110">An **indexer** in Azure Search is a crawler that extracts searchable data and metadata from an external data source and populates an index based on field-to-field mappings between the index and your data source.</span></span> <span data-ttu-id="b616d-111">This approach is sometimes referred to as a 'pull model' because the service pulls data in without you having to write any code that pushes data to an index.</span><span class="sxs-lookup"><span data-stu-id="b616d-111">This approach is sometimes referred to as a 'pull model' because the service pulls data in without you having to write any code that pushes data to an index.</span></span>

<span data-ttu-id="b616d-112">You can use an indexer as the sole means for data ingestion, or use a combination of techniques that include the use of an indexer for loading just some of the fields in your index.</span><span class="sxs-lookup"><span data-stu-id="b616d-112">You can use an indexer as the sole means for data ingestion, or use a combination of techniques that include the use of an indexer for loading just some of the fields in your index.</span></span>

<span data-ttu-id="b616d-113">You can run indexers on demand or on a recurring data refresh schedule that runs as often as every fifteen minutes.</span><span class="sxs-lookup"><span data-stu-id="b616d-113">You can run indexers on demand or on a recurring data refresh schedule that runs as often as every fifteen minutes.</span></span> <span data-ttu-id="b616d-114">More frequent updates require a push model that simultaneously updates data in both Azure Search and your external data source.</span><span class="sxs-lookup"><span data-stu-id="b616d-114">More frequent updates require a push model that simultaneously updates data in both Azure Search and your external data source.</span></span>

## <a name="approaches-for-creating-and-managing-indexers"></a><span data-ttu-id="b616d-115">Approaches for creating and managing indexers</span><span class="sxs-lookup"><span data-stu-id="b616d-115">Approaches for creating and managing indexers</span></span>
<span data-ttu-id="b616d-116">For generally available indexers like Azure SQL or DocumentDB, you can create and manage indexers using these approaches:</span><span class="sxs-lookup"><span data-stu-id="b616d-116">For generally available indexers like Azure SQL or DocumentDB, you can create and manage indexers using these approaches:</span></span>

* [<span data-ttu-id="b616d-117">Portal > Import Data Wizard </span><span class="sxs-lookup"><span data-stu-id="b616d-117">Portal > Import Data Wizard </span></span>](search-get-started-portal.md)
* [<span data-ttu-id="b616d-118">Service REST API</span><span class="sxs-lookup"><span data-stu-id="b616d-118">Service REST API</span></span>](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [<span data-ttu-id="b616d-119">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="b616d-119">.NET SDK</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a><span data-ttu-id="b616d-120">Basic configuration steps</span><span class="sxs-lookup"><span data-stu-id="b616d-120">Basic configuration steps</span></span>
<span data-ttu-id="b616d-121">Indexers can offer features that are unique to the data source.</span><span class="sxs-lookup"><span data-stu-id="b616d-121">Indexers can offer features that are unique to the data source.</span></span> <span data-ttu-id="b616d-122">In this respect, some aspects of indexer or data source configuration will vary by indexer type.</span><span class="sxs-lookup"><span data-stu-id="b616d-122">In this respect, some aspects of indexer or data source configuration will vary by indexer type.</span></span> <span data-ttu-id="b616d-123">However, all indexers share the same basic composition and requirements.</span><span class="sxs-lookup"><span data-stu-id="b616d-123">However, all indexers share the same basic composition and requirements.</span></span> <span data-ttu-id="b616d-124">Steps that are common to all indexers are covered below.</span><span class="sxs-lookup"><span data-stu-id="b616d-124">Steps that are common to all indexers are covered below.</span></span>

### <a name="step-1-create-an-index"></a><span data-ttu-id="b616d-125">Step 1: Create an index</span><span class="sxs-lookup"><span data-stu-id="b616d-125">Step 1: Create an index</span></span>
<span data-ttu-id="b616d-126">An indexer will automate some tasks related to data ingestion, but creating an index is not one of them.</span><span class="sxs-lookup"><span data-stu-id="b616d-126">An indexer will automate some tasks related to data ingestion, but creating an index is not one of them.</span></span> <span data-ttu-id="b616d-127">As a prerequisite, you must have a predefined index with fields that match those in your external data source.</span><span class="sxs-lookup"><span data-stu-id="b616d-127">As a prerequisite, you must have a predefined index with fields that match those in your external data source.</span></span> <span data-ttu-id="b616d-128">For more information about structuring an index, see [Create an Index (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span><span class="sxs-lookup"><span data-stu-id="b616d-128">For more information about structuring an index, see [Create an Index (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn798941.aspx).</span></span>

### <a name="step-2-create-a-data-source"></a><span data-ttu-id="b616d-129">Step 2: Create a data source</span><span class="sxs-lookup"><span data-stu-id="b616d-129">Step 2: Create a data source</span></span>
<span data-ttu-id="b616d-130">An indexer pulls data from a **data source** which holds information such as a connection string.</span><span class="sxs-lookup"><span data-stu-id="b616d-130">An indexer pulls data from a **data source** which holds information such as a connection string.</span></span> <span data-ttu-id="b616d-131">Currently the following data sources are supported:</span><span class="sxs-lookup"><span data-stu-id="b616d-131">Currently the following data sources are supported:</span></span>

* [<span data-ttu-id="b616d-132">Azure SQL Database or SQL Server on an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="b616d-132">Azure SQL Database or SQL Server on an Azure virtual machine</span></span>](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [<span data-ttu-id="b616d-133">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b616d-133">DocumentDB</span></span>](search-howto-index-documentdb.md)
* <span data-ttu-id="b616d-134">[Azure Blob storage](search-howto-indexing-azure-blob-storage.md), used to extract text from PDF, Office documents, HTML, or XML</span><span class="sxs-lookup"><span data-stu-id="b616d-134">[Azure Blob storage](search-howto-indexing-azure-blob-storage.md), used to extract text from PDF, Office documents, HTML, or XML</span></span>
* [<span data-ttu-id="b616d-135">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="b616d-135">Azure Table Storage</span></span>](search-howto-indexing-azure-tables.md)

<span data-ttu-id="b616d-136">Data sources are configured and managed independently of the indexers that use them, which means a data source can be used by multiple indexers to load more than one index at a time.</span><span class="sxs-lookup"><span data-stu-id="b616d-136">Data sources are configured and managed independently of the indexers that use them, which means a data source can be used by multiple indexers to load more than one index at a time.</span></span>

### <a name="step-3create-and-schedule-the-indexer"></a><span data-ttu-id="b616d-137">Step 3:Create and schedule the indexer</span><span class="sxs-lookup"><span data-stu-id="b616d-137">Step 3:Create and schedule the indexer</span></span>
<span data-ttu-id="b616d-138">The indexer definition is a construct specifying the index, data source, and a schedule.</span><span class="sxs-lookup"><span data-stu-id="b616d-138">The indexer definition is a construct specifying the index, data source, and a schedule.</span></span> <span data-ttu-id="b616d-139">An indexer can reference a data source from another service, as long as that data source is from the same subscription.</span><span class="sxs-lookup"><span data-stu-id="b616d-139">An indexer can reference a data source from another service, as long as that data source is from the same subscription.</span></span> <span data-ttu-id="b616d-140">For more information about structuring an indexer, see [Create Indexer (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx).</span><span class="sxs-lookup"><span data-stu-id="b616d-140">For more information about structuring an indexer, see [Create Indexer (Azure Search REST API)](https://msdn.microsoft.com/library/azure/dn946899.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b616d-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="b616d-141">Next steps</span></span>
<span data-ttu-id="b616d-142">Now that you have the basic idea, the next step is to review requirements and tasks specific to each data source type.</span><span class="sxs-lookup"><span data-stu-id="b616d-142">Now that you have the basic idea, the next step is to review requirements and tasks specific to each data source type.</span></span>

* [<span data-ttu-id="b616d-143">Azure SQL Database or SQL Server on an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="b616d-143">Azure SQL Database or SQL Server on an Azure virtual machine</span></span>](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [<span data-ttu-id="b616d-144">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b616d-144">DocumentDB</span></span>](search-howto-index-documentdb.md)
* <span data-ttu-id="b616d-145">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md), used to extract text from PDF, Office documents, HTML, or XML</span><span class="sxs-lookup"><span data-stu-id="b616d-145">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md), used to extract text from PDF, Office documents, HTML, or XML</span></span>
* [<span data-ttu-id="b616d-146">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="b616d-146">Azure Table Storage</span></span>](search-howto-indexing-azure-tables.md)
* [<span data-ttu-id="b616d-147">Indexing CSV blobs using the Azure Search Blob indexer (Preview)</span><span class="sxs-lookup"><span data-stu-id="b616d-147">Indexing CSV blobs using the Azure Search Blob indexer (Preview)</span></span>](search-howto-index-csv-blobs.md)
* [<span data-ttu-id="b616d-148">Indexing JSON blobs with Azure Search Blob indexer (Preview)</span><span class="sxs-lookup"><span data-stu-id="b616d-148">Indexing JSON blobs with Azure Search Blob indexer (Preview)</span></span>](search-howto-index-json-blobs.md)
