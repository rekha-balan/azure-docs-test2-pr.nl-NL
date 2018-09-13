---
title: Indexing Azure Table storage with Azure Search | Microsoft Docs
description: Learn how to index data stored in Azure Table storage with Azure Search
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 7679aa86aa24396d9cd7cf84a8cafe7950ad6d62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562778"
---
# <a name="index-azure-table-storage-with-azure-search"></a><span data-ttu-id="1b4c4-103">Index Azure Table storage with Azure Search</span><span class="sxs-lookup"><span data-stu-id="1b4c4-103">Index Azure Table storage with Azure Search</span></span>
<span data-ttu-id="1b4c4-104">This article shows how to use Azure Search to index data stored in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-104">This article shows how to use Azure Search to index data stored in Azure Table storage.</span></span>

## <a name="set-up-azure-table-storage-indexing"></a><span data-ttu-id="1b4c4-105">Set up Azure Table storage indexing</span><span class="sxs-lookup"><span data-stu-id="1b4c4-105">Set up Azure Table storage indexing</span></span>

<span data-ttu-id="1b4c4-106">You can set up an Azure Table storage indexer by using these resources:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-106">You can set up an Azure Table storage indexer by using these resources:</span></span>

* [<span data-ttu-id="1b4c4-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1b4c4-107">Azure portal</span></span>](https://ms.portal.azure.com)
* <span data-ttu-id="1b4c4-108">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span><span class="sxs-lookup"><span data-stu-id="1b4c4-108">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span></span>
* <span data-ttu-id="1b4c4-109">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span><span class="sxs-lookup"><span data-stu-id="1b4c4-109">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span></span>

<span data-ttu-id="1b4c4-110">Here we demonstrate the flow by using the REST API.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-110">Here we demonstrate the flow by using the REST API.</span></span> 

### <a name="step-1-create-a-datasource"></a><span data-ttu-id="1b4c4-111">Step 1: Create a datasource</span><span class="sxs-lookup"><span data-stu-id="1b4c4-111">Step 1: Create a datasource</span></span>

<span data-ttu-id="1b4c4-112">A datasource specifies which data to index, the credentials needed to access the data, and the policies that enable Azure Search to efficiently identify changes in the data.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-112">A datasource specifies which data to index, the credentials needed to access the data, and the policies that enable Azure Search to efficiently identify changes in the data.</span></span>

<span data-ttu-id="1b4c4-113">For table indexing, the datasource must have the following properties:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-113">For table indexing, the datasource must have the following properties:</span></span>

- <span data-ttu-id="1b4c4-114">**name** is the unique name of the datasource within your search service.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-114">**name** is the unique name of the datasource within your search service.</span></span>
- <span data-ttu-id="1b4c4-115">**type** must be `azuretable`.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-115">**type** must be `azuretable`.</span></span>
- <span data-ttu-id="1b4c4-116">**credentials** parameter contains the storage account connection string.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-116">**credentials** parameter contains the storage account connection string.</span></span> <span data-ttu-id="1b4c4-117">See the [Specify credentials](#Credentials) section for details.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-117">See the [Specify credentials](#Credentials) section for details.</span></span>
- <span data-ttu-id="1b4c4-118">**container** sets the table name and an optional query.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-118">**container** sets the table name and an optional query.</span></span>
    - <span data-ttu-id="1b4c4-119">Specify the table name by using the `name` parameter.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-119">Specify the table name by using the `name` parameter.</span></span>
    - <span data-ttu-id="1b4c4-120">Optionally, specify a query by using the `query` parameter.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-120">Optionally, specify a query by using the `query` parameter.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="1b4c4-121">Whenever possible, use a filter on PartitionKey for better performance.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-121">Whenever possible, use a filter on PartitionKey for better performance.</span></span> <span data-ttu-id="1b4c4-122">Any other query does a full table scan, resulting in poor performance for large tables.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-122">Any other query does a full table scan, resulting in poor performance for large tables.</span></span> <span data-ttu-id="1b4c4-123">See the [Performance considerations](#Performance) section.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-123">See the [Performance considerations](#Performance) section.</span></span>


<span data-ttu-id="1b4c4-124">To create a datasource:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-124">To create a datasource:</span></span>

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

<span data-ttu-id="1b4c4-125">For more information on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-125">For more information on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span></span>

<a name="Credentials"></a>
#### <a name="ways-to-specify-credentials"></a><span data-ttu-id="1b4c4-126">Ways to specify credentials</span><span class="sxs-lookup"><span data-stu-id="1b4c4-126">Ways to specify credentials</span></span> ####

<span data-ttu-id="1b4c4-127">You can provide the credentials for the table in one of these ways:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-127">You can provide the credentials for the table in one of these ways:</span></span> 

- <span data-ttu-id="1b4c4-128">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` You can get the connection string from the Azure portal by going to the **Storage account blade** > **Settings** > **Keys** (for classic storage accounts) or **Settings** > **Access keys** (for Azure Resource Manager storage accounts).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-128">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` You can get the connection string from the Azure portal by going to the **Storage account blade** > **Settings** > **Keys** (for classic storage accounts) or **Settings** > **Access keys** (for Azure Resource Manager storage accounts).</span></span>
- <span data-ttu-id="1b4c4-129">**Storage account shared access signature connection string**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=t&sp=rl` The shared access signature should have the list and read permissions on containers (tables in this case) and objects (table rows).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-129">**Storage account shared access signature connection string**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=t&sp=rl` The shared access signature should have the list and read permissions on containers (tables in this case) and objects (table rows).</span></span>
-  <span data-ttu-id="1b4c4-130">**Table shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<the signature>&se=<the validity end time>&sp=r` The shared access signature should have query (read) permissions on the table.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-130">**Table shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<the signature>&se=<the validity end time>&sp=r` The shared access signature should have query (read) permissions on the table.</span></span>

<span data-ttu-id="1b4c4-131">For more information on storage shared access signatures, see [Using shared access signatures](../storage/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-131">For more information on storage shared access signatures, see [Using shared access signatures](../storage/storage-dotnet-shared-access-signature-part-1.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1b4c4-132">If you use shared access signature credentials, you will need to update the datasource credentials periodically with renewed signatures to prevent their expiration.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-132">If you use shared access signature credentials, you will need to update the datasource credentials periodically with renewed signatures to prevent their expiration.</span></span> <span data-ttu-id="1b4c4-133">If shared access signature credentials expire, the indexer fails with an error message similar to "Credentials provided in the connection string are invalid or have expired."</span><span class="sxs-lookup"><span data-stu-id="1b4c4-133">If shared access signature credentials expire, the indexer fails with an error message similar to "Credentials provided in the connection string are invalid or have expired."</span></span>  

### <a name="step-2-create-an-index"></a><span data-ttu-id="1b4c4-134">Step 2: Create an index</span><span class="sxs-lookup"><span data-stu-id="1b4c4-134">Step 2: Create an index</span></span>
<span data-ttu-id="1b4c4-135">The index specifies the fields in a document, the attributes, and other constructs that shape the search experience.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-135">The index specifies the fields in a document, the attributes, and other constructs that shape the search experience.</span></span>

<span data-ttu-id="1b4c4-136">To create an index:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-136">To create an index:</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

<span data-ttu-id="1b4c4-137">For more information on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-137">For more information on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index).</span></span>

### <a name="step-3-create-an-indexer"></a><span data-ttu-id="1b4c4-138">Step 3: Create an indexer</span><span class="sxs-lookup"><span data-stu-id="1b4c4-138">Step 3: Create an indexer</span></span>
<span data-ttu-id="1b4c4-139">An indexer connects a datasource with a target search index and provides a schedule to automate the data refresh.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-139">An indexer connects a datasource with a target search index and provides a schedule to automate the data refresh.</span></span> 

<span data-ttu-id="1b4c4-140">After the index and datasource are created, you're ready to create the indexer:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-140">After the index and datasource are created, you're ready to create the indexer:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

<span data-ttu-id="1b4c4-141">This indexer runs every two hours.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-141">This indexer runs every two hours.</span></span> <span data-ttu-id="1b4c4-142">(The schedule interval is set to "PT2H".) To run an indexer every 30 minutes, set the interval to "PT30M".</span><span class="sxs-lookup"><span data-stu-id="1b4c4-142">(The schedule interval is set to "PT2H".) To run an indexer every 30 minutes, set the interval to "PT30M".</span></span> <span data-ttu-id="1b4c4-143">The shortest supported interval is five minutes.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-143">The shortest supported interval is five minutes.</span></span> <span data-ttu-id="1b4c4-144">The schedule is optional; if omitted, an indexer runs only once when it's created.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-144">The schedule is optional; if omitted, an indexer runs only once when it's created.</span></span> <span data-ttu-id="1b4c4-145">However, you can run an indexer on demand at any time.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-145">However, you can run an indexer on demand at any time.</span></span>   

<span data-ttu-id="1b4c4-146">For more information on the Create Indexer API, see [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-146">For more information on the Create Indexer API, see [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span></span>

## <a name="deal-with-different-field-names"></a><span data-ttu-id="1b4c4-147">Deal with different field names</span><span class="sxs-lookup"><span data-stu-id="1b4c4-147">Deal with different field names</span></span>
<span data-ttu-id="1b4c4-148">Sometimes, the field names in your existing index are different from the property names in your table.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-148">Sometimes, the field names in your existing index are different from the property names in your table.</span></span> <span data-ttu-id="1b4c4-149">You can use field mappings to map the property names from the table to the field names in your search index.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-149">You can use field mappings to map the property names from the table to the field names in your search index.</span></span> <span data-ttu-id="1b4c4-150">To learn more about field mappings, see [Azure Search indexer field mappings bridge the differences between datasources and search indexes](search-indexer-field-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-150">To learn more about field mappings, see [Azure Search indexer field mappings bridge the differences between datasources and search indexes](search-indexer-field-mappings.md).</span></span>

## <a name="handle-document-keys"></a><span data-ttu-id="1b4c4-151">Handle document keys</span><span class="sxs-lookup"><span data-stu-id="1b4c4-151">Handle document keys</span></span>
<span data-ttu-id="1b4c4-152">In Azure Search, the document key uniquely identifies a document.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-152">In Azure Search, the document key uniquely identifies a document.</span></span> <span data-ttu-id="1b4c4-153">Every search index must have exactly one key field of type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-153">Every search index must have exactly one key field of type `Edm.String`.</span></span> <span data-ttu-id="1b4c4-154">The key field is required for each document that is being added to the index.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-154">The key field is required for each document that is being added to the index.</span></span> <span data-ttu-id="1b4c4-155">(In fact, it's the only required field.)</span><span class="sxs-lookup"><span data-stu-id="1b4c4-155">(In fact, it's the only required field.)</span></span>

<span data-ttu-id="1b4c4-156">Because table rows have a compound key, Azure Search generates a synthetic field called `Key` that is a concatenation of partition key and row key values.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-156">Because table rows have a compound key, Azure Search generates a synthetic field called `Key` that is a concatenation of partition key and row key values.</span></span> <span data-ttu-id="1b4c4-157">For example, if a row’s PartitionKey is `PK1` and RowKey is `RK1`, then the `Key` field's value is `PK1RK1`.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-157">For example, if a row’s PartitionKey is `PK1` and RowKey is `RK1`, then the `Key` field's value is `PK1RK1`.</span></span>

> [!NOTE]
> <span data-ttu-id="1b4c4-158">The `Key` value may contain characters that are invalid in document keys, such as dashes.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-158">The `Key` value may contain characters that are invalid in document keys, such as dashes.</span></span> <span data-ttu-id="1b4c4-159">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-159">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction).</span></span> <span data-ttu-id="1b4c4-160">If you do this, remember to also use URL-safe Base64 encoding when passing document keys in API calls such as Lookup.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-160">If you do this, remember to also use URL-safe Base64 encoding when passing document keys in API calls such as Lookup.</span></span>
>
>

## <a name="incremental-indexing-and-deletion-detection"></a><span data-ttu-id="1b4c4-161">Incremental indexing and deletion detection</span><span class="sxs-lookup"><span data-stu-id="1b4c4-161">Incremental indexing and deletion detection</span></span>
<span data-ttu-id="1b4c4-162">When you set up a table indexer to run on a schedule, it reindexes only new or updated rows, as determined by a row’s `Timestamp` value.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-162">When you set up a table indexer to run on a schedule, it reindexes only new or updated rows, as determined by a row’s `Timestamp` value.</span></span> <span data-ttu-id="1b4c4-163">You don’t have to specify a change detection policy.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-163">You don’t have to specify a change detection policy.</span></span> <span data-ttu-id="1b4c4-164">Incremental indexing is enabled for you automatically.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-164">Incremental indexing is enabled for you automatically.</span></span>

<span data-ttu-id="1b4c4-165">To indicate that certain documents must be removed from the index, you can use a soft delete strategy.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-165">To indicate that certain documents must be removed from the index, you can use a soft delete strategy.</span></span> <span data-ttu-id="1b4c4-166">Instead of deleting a row, add a property to indicate that it's deleted, and set up a soft deletion detection policy on the datasource.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-166">Instead of deleting a row, add a property to indicate that it's deleted, and set up a soft deletion detection policy on the datasource.</span></span> <span data-ttu-id="1b4c4-167">For example, the following policy considers that a row is deleted if the row has a property `IsDeleted` with the value `"true"`:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-167">For example, the following policy considers that a row is deleted if the row has a property `IsDeleted` with the value `"true"`:</span></span>

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a><span data-ttu-id="1b4c4-168">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="1b4c4-168">Performance considerations</span></span>

<span data-ttu-id="1b4c4-169">By default, Azure Search uses the following query filter: `Timestamp >= HighWaterMarkValue`.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-169">By default, Azure Search uses the following query filter: `Timestamp >= HighWaterMarkValue`.</span></span> <span data-ttu-id="1b4c4-170">Because Azure tables don’t have a secondary index on the `Timestamp` field, this type of query requires a full table scan and is therefore slow for large tables.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-170">Because Azure tables don’t have a secondary index on the `Timestamp` field, this type of query requires a full table scan and is therefore slow for large tables.</span></span>


<span data-ttu-id="1b4c4-171">Here are two possible approaches for improving table indexing performance.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-171">Here are two possible approaches for improving table indexing performance.</span></span> <span data-ttu-id="1b4c4-172">Both of these approaches rely on using table partitions:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-172">Both of these approaches rely on using table partitions:</span></span> 

- <span data-ttu-id="1b4c4-173">If your data can naturally be partitioned into several partition ranges, create a datasource and a corresponding indexer for each partition range.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-173">If your data can naturally be partitioned into several partition ranges, create a datasource and a corresponding indexer for each partition range.</span></span> <span data-ttu-id="1b4c4-174">Each indexer now has to process only a specific partition range, resulting in better query performance.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-174">Each indexer now has to process only a specific partition range, resulting in better query performance.</span></span> <span data-ttu-id="1b4c4-175">If the data that needs to be indexed has a small number of fixed partitions, even better: each indexer only does a partition scan.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-175">If the data that needs to be indexed has a small number of fixed partitions, even better: each indexer only does a partition scan.</span></span> <span data-ttu-id="1b4c4-176">For example, to create a datasource for processing a partition range with keys from `000` to `100`, use a query like this:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-176">For example, to create a datasource for processing a partition range with keys from `000` to `100`, use a query like this:</span></span> 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- <span data-ttu-id="1b4c4-177">If your data is partitioned by time (for example, you create a new partition every day or week), consider the following approach:</span><span class="sxs-lookup"><span data-stu-id="1b4c4-177">If your data is partitioned by time (for example, you create a new partition every day or week), consider the following approach:</span></span> 
    - <span data-ttu-id="1b4c4-178">Use a query of the form: `(PartitionKey ge <TimeStamp>) and (other filters)`.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-178">Use a query of the form: `(PartitionKey ge <TimeStamp>) and (other filters)`.</span></span> 
    - <span data-ttu-id="1b4c4-179">Monitor indexer progress by using [Get Indexer Status API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status), and periodically update the `<TimeStamp>` condition of the query based on the latest successful high-water-mark value.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-179">Monitor indexer progress by using [Get Indexer Status API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status), and periodically update the `<TimeStamp>` condition of the query based on the latest successful high-water-mark value.</span></span> 
    - <span data-ttu-id="1b4c4-180">With this approach, if you need to trigger a complete reindexing, you need to reset the datasource query in addition to resetting the indexer.</span><span class="sxs-lookup"><span data-stu-id="1b4c4-180">With this approach, if you need to trigger a complete reindexing, you need to reset the datasource query in addition to resetting the indexer.</span></span> 


## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="1b4c4-181">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="1b4c4-181">Help us make Azure Search better</span></span>
<span data-ttu-id="1b4c4-182">If you have feature requests or ideas for improvements, submit them on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="1b4c4-182">If you have feature requests or ideas for improvements, submit them on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
