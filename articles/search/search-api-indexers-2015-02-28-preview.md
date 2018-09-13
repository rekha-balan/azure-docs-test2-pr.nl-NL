---
title: 'Indexer Operations (Azure Search Service REST API: 2015-02-28-Preview) | Microsoft Docs'
description: 'Indexer Operations (Azure Search Service REST API: 2015-02-28-Preview)'
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 11/01/2016
ms.author: eugenesh
ms.openlocfilehash: 801a9d0e92a248d2e9843f13cfce74b948cf0d4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554603"
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a><span data-ttu-id="b066e-103">Indexer Operations (Azure Search Service REST API: 2015-02-28-Preview)</span><span class="sxs-lookup"><span data-stu-id="b066e-103">Indexer Operations (Azure Search Service REST API: 2015-02-28-Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="b066e-104">This article describes indexers in the [2015-02-28-Preview REST API](search-api-2015-02-28-preview.md).</span><span class="sxs-lookup"><span data-stu-id="b066e-104">This article describes indexers in the [2015-02-28-Preview REST API](search-api-2015-02-28-preview.md).</span></span> <span data-ttu-id="b066e-105">This API version adds preview versions of Azure Blob Storage indexer with document extraction and Azure Table Storage indexer, plus other improvements.</span><span class="sxs-lookup"><span data-stu-id="b066e-105">This API version adds preview versions of Azure Blob Storage indexer with document extraction and Azure Table Storage indexer, plus other improvements.</span></span> <span data-ttu-id="b066e-106">The API also supports generally available (GA) indexers, including indexers for Azure SQL Database, SQL Server on Azure VMs, and Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b066e-106">The API also supports generally available (GA) indexers, including indexers for Azure SQL Database, SQL Server on Azure VMs, and Azure DocumentDB.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b066e-107">Overview</span><span class="sxs-lookup"><span data-stu-id="b066e-107">Overview</span></span>
<span data-ttu-id="b066e-108">Azure Search can integrate directly with some common data sources, removing the need to write code to index your data.</span><span class="sxs-lookup"><span data-stu-id="b066e-108">Azure Search can integrate directly with some common data sources, removing the need to write code to index your data.</span></span> <span data-ttu-id="b066e-109">To set up this up, you can call the Azure Search API to create and manage **indexers** and **data sources**.</span><span class="sxs-lookup"><span data-stu-id="b066e-109">To set up this up, you can call the Azure Search API to create and manage **indexers** and **data sources**.</span></span> 

<span data-ttu-id="b066e-110">An **indexer** is a resource that connects data sources with target search indexes.</span><span class="sxs-lookup"><span data-stu-id="b066e-110">An **indexer** is a resource that connects data sources with target search indexes.</span></span> <span data-ttu-id="b066e-111">An indexer is used in the following ways:</span><span class="sxs-lookup"><span data-stu-id="b066e-111">An indexer is used in the following ways:</span></span> 

* <span data-ttu-id="b066e-112">Perform a one-time copy of the data to populate an index.</span><span class="sxs-lookup"><span data-stu-id="b066e-112">Perform a one-time copy of the data to populate an index.</span></span>
* <span data-ttu-id="b066e-113">Sync an index with changes in the data source on a schedule.</span><span class="sxs-lookup"><span data-stu-id="b066e-113">Sync an index with changes in the data source on a schedule.</span></span> <span data-ttu-id="b066e-114">The schedule is part of the indexer definition.</span><span class="sxs-lookup"><span data-stu-id="b066e-114">The schedule is part of the indexer definition.</span></span>
* <span data-ttu-id="b066e-115">Invoke on-demand to update an index as needed.</span><span class="sxs-lookup"><span data-stu-id="b066e-115">Invoke on-demand to update an index as needed.</span></span> 

<span data-ttu-id="b066e-116">An **indexer** is useful when you want regular updates to an index.</span><span class="sxs-lookup"><span data-stu-id="b066e-116">An **indexer** is useful when you want regular updates to an index.</span></span> <span data-ttu-id="b066e-117">You can either set up an inline schedule as part of an indexer definition, or run it on demand using [Run Indexer](#RunIndexer).</span><span class="sxs-lookup"><span data-stu-id="b066e-117">You can either set up an inline schedule as part of an indexer definition, or run it on demand using [Run Indexer](#RunIndexer).</span></span> 

<span data-ttu-id="b066e-118">A **data source** specifies what data needs to be indexed, credentials to access the data, and policies to enable Azure Search to efficiently identify changes in the data (such as modified or deleted rows in a database table).</span><span class="sxs-lookup"><span data-stu-id="b066e-118">A **data source** specifies what data needs to be indexed, credentials to access the data, and policies to enable Azure Search to efficiently identify changes in the data (such as modified or deleted rows in a database table).</span></span> <span data-ttu-id="b066e-119">It's defined as an independent resource so that it can be used by multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="b066e-119">It's defined as an independent resource so that it can be used by multiple indexers.</span></span>

<span data-ttu-id="b066e-120">The following data sources are currently supported:</span><span class="sxs-lookup"><span data-stu-id="b066e-120">The following data sources are currently supported:</span></span>

* <span data-ttu-id="b066e-121">**Azure SQL Database** and **SQL Server on Azure VMs**.</span><span class="sxs-lookup"><span data-stu-id="b066e-121">**Azure SQL Database** and **SQL Server on Azure VMs**.</span></span> <span data-ttu-id="b066e-122">For a targeted walk-through, see [this article](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md).</span><span class="sxs-lookup"><span data-stu-id="b066e-122">For a targeted walk-through, see [this article](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md).</span></span> 
* <span data-ttu-id="b066e-123">**Azure DocumentDB**.</span><span class="sxs-lookup"><span data-stu-id="b066e-123">**Azure DocumentDB**.</span></span> <span data-ttu-id="b066e-124">For a targeted walk-through, see [this article](search-howto-index-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="b066e-124">For a targeted walk-through, see [this article](search-howto-index-documentdb.md).</span></span> 
* <span data-ttu-id="b066e-125">**Azure Blob Storage**, including the following document formats: PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, ZIP, and plain text files (including JSON).</span><span class="sxs-lookup"><span data-stu-id="b066e-125">**Azure Blob Storage**, including the following document formats: PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, ZIP, and plain text files (including JSON).</span></span> <span data-ttu-id="b066e-126">For  a targeted walk-through, see [this article](search-howto-indexing-azure-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b066e-126">For  a targeted walk-through, see [this article](search-howto-indexing-azure-blob-storage.md).</span></span>
* <span data-ttu-id="b066e-127">**Azure Table Storage**.</span><span class="sxs-lookup"><span data-stu-id="b066e-127">**Azure Table Storage**.</span></span> <span data-ttu-id="b066e-128">For a targeted walk-through, see [this article](search-howto-indexing-azure-tables.md).</span><span class="sxs-lookup"><span data-stu-id="b066e-128">For a targeted walk-through, see [this article](search-howto-indexing-azure-tables.md).</span></span>

<span data-ttu-id="b066e-129">We're considering adding support for additional data sources in the future.</span><span class="sxs-lookup"><span data-stu-id="b066e-129">We're considering adding support for additional data sources in the future.</span></span> <span data-ttu-id="b066e-130">To help us prioritize these decisions, please provide your feedback on the [Azure Search feedback forum](http://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="b066e-130">To help us prioritize these decisions, please provide your feedback on the [Azure Search feedback forum](http://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="b066e-131">See [Service Limits](search-limits-quotas-capacity.md) for maximum limits related to indexer and data source resources.</span><span class="sxs-lookup"><span data-stu-id="b066e-131">See [Service Limits](search-limits-quotas-capacity.md) for maximum limits related to indexer and data source resources.</span></span>

## <a name="typical-usage-flow"></a><span data-ttu-id="b066e-132">Typical Usage Flow</span><span class="sxs-lookup"><span data-stu-id="b066e-132">Typical Usage Flow</span></span>
<span data-ttu-id="b066e-133">You can create and manage indexers and data sources via simple HTTP requests (POST, GET, PUT, DELETE) against a given `data source` or `indexer` resource.</span><span class="sxs-lookup"><span data-stu-id="b066e-133">You can create and manage indexers and data sources via simple HTTP requests (POST, GET, PUT, DELETE) against a given `data source` or `indexer` resource.</span></span>

<span data-ttu-id="b066e-134">Setting up automatic indexing is typically a four step process:</span><span class="sxs-lookup"><span data-stu-id="b066e-134">Setting up automatic indexing is typically a four step process:</span></span>

1. <span data-ttu-id="b066e-135">Identify the data source that contains the data that needs to be indexed.</span><span class="sxs-lookup"><span data-stu-id="b066e-135">Identify the data source that contains the data that needs to be indexed.</span></span> <span data-ttu-id="b066e-136">Keep in mind that Azure Search may not support all of the data types present in your data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-136">Keep in mind that Azure Search may not support all of the data types present in your data source.</span></span> <span data-ttu-id="b066e-137">See [Supported data types](https://msdn.microsoft.com/library/azure/dn798938.aspx) for the list.</span><span class="sxs-lookup"><span data-stu-id="b066e-137">See [Supported data types](https://msdn.microsoft.com/library/azure/dn798938.aspx) for the list.</span></span>
2. <span data-ttu-id="b066e-138">Create an Azure Search index whose schema is compatible with your data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-138">Create an Azure Search index whose schema is compatible with your data source.</span></span>
3. <span data-ttu-id="b066e-139">Create an Azure Search data source as described in [Create Data Source](#CreateDataSource).</span><span class="sxs-lookup"><span data-stu-id="b066e-139">Create an Azure Search data source as described in [Create Data Source](#CreateDataSource).</span></span>
4. <span data-ttu-id="b066e-140">Create an Azure Search indexer as described [Create Indexer](#CreateIndexer).</span><span class="sxs-lookup"><span data-stu-id="b066e-140">Create an Azure Search indexer as described [Create Indexer](#CreateIndexer).</span></span>

<span data-ttu-id="b066e-141">You should plan on creating one indexer for every target index and data source combination.</span><span class="sxs-lookup"><span data-stu-id="b066e-141">You should plan on creating one indexer for every target index and data source combination.</span></span> <span data-ttu-id="b066e-142">You can have multiple indexers writing into the same index, and you can reuse the same data source for multiple indexers.</span><span class="sxs-lookup"><span data-stu-id="b066e-142">You can have multiple indexers writing into the same index, and you can reuse the same data source for multiple indexers.</span></span> <span data-ttu-id="b066e-143">However, an indexer can only consume one data source at a time, and can only write to a single index.</span><span class="sxs-lookup"><span data-stu-id="b066e-143">However, an indexer can only consume one data source at a time, and can only write to a single index.</span></span> 

<span data-ttu-id="b066e-144">After creating an indexer, you can retrieve its execution status using the [Get Indexer Status](#GetIndexerStatus) operation.</span><span class="sxs-lookup"><span data-stu-id="b066e-144">After creating an indexer, you can retrieve its execution status using the [Get Indexer Status](#GetIndexerStatus) operation.</span></span> <span data-ttu-id="b066e-145">You can also run an indexer at any time (instead of or in addition to running it periodically on a schedule) using the [Run Indexer](#RunIndexer) operation.</span><span class="sxs-lookup"><span data-stu-id="b066e-145">You can also run an indexer at any time (instead of or in addition to running it periodically on a schedule) using the [Run Indexer](#RunIndexer) operation.</span></span>

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a><span data-ttu-id="b066e-146">Create Data Source</span><span class="sxs-lookup"><span data-stu-id="b066e-146">Create Data Source</span></span>
<span data-ttu-id="b066e-147">In Azure Search, a data source is used with indexers, providing the connection information for ad hoc or scheduled data refresh of a target index.</span><span class="sxs-lookup"><span data-stu-id="b066e-147">In Azure Search, a data source is used with indexers, providing the connection information for ad hoc or scheduled data refresh of a target index.</span></span> <span data-ttu-id="b066e-148">You can create a new data source within an Azure Search service using an HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="b066e-148">You can create a new data source within an Azure Search service using an HTTP POST request.</span></span>

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="b066e-149">Alternatively, you can use PUT and specify the data source name on the URI.</span><span class="sxs-lookup"><span data-stu-id="b066e-149">Alternatively, you can use PUT and specify the data source name on the URI.</span></span> <span data-ttu-id="b066e-150">If the data source does not exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="b066e-150">If the data source does not exist, it will be created.</span></span>

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> <span data-ttu-id="b066e-151">The maximum number of data sources allowed varies by pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b066e-151">The maximum number of data sources allowed varies by pricing tier.</span></span> <span data-ttu-id="b066e-152">The free service allows up to 3 data sources.</span><span class="sxs-lookup"><span data-stu-id="b066e-152">The free service allows up to 3 data sources.</span></span> <span data-ttu-id="b066e-153">Standard service allows 50 data sources.</span><span class="sxs-lookup"><span data-stu-id="b066e-153">Standard service allows 50 data sources.</span></span> <span data-ttu-id="b066e-154">See [Service Limits](search-limits-quotas-capacity.md) for details.</span><span class="sxs-lookup"><span data-stu-id="b066e-154">See [Service Limits](search-limits-quotas-capacity.md) for details.</span></span>
> 
> 

<span data-ttu-id="b066e-155">**Request**</span><span class="sxs-lookup"><span data-stu-id="b066e-155">**Request**</span></span>

<span data-ttu-id="b066e-156">HTTPS is required for all service requests.</span><span class="sxs-lookup"><span data-stu-id="b066e-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="b066e-157">The **Create Data Source** request can be constructed using either a POST or PUT method.</span><span class="sxs-lookup"><span data-stu-id="b066e-157">The **Create Data Source** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="b066e-158">When using POST, you must provide a data source name in the request body along with the data source definition.</span><span class="sxs-lookup"><span data-stu-id="b066e-158">When using POST, you must provide a data source name in the request body along with the data source definition.</span></span> <span data-ttu-id="b066e-159">With PUT, the name is part of the URL.</span><span class="sxs-lookup"><span data-stu-id="b066e-159">With PUT, the name is part of the URL.</span></span> <span data-ttu-id="b066e-160">If the data source doesn't exist, it is created.</span><span class="sxs-lookup"><span data-stu-id="b066e-160">If the data source doesn't exist, it is created.</span></span> <span data-ttu-id="b066e-161">If it already exists, it is updated to the new definition.</span><span class="sxs-lookup"><span data-stu-id="b066e-161">If it already exists, it is updated to the new definition.</span></span> 

<span data-ttu-id="b066e-162">The data source name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span><span class="sxs-lookup"><span data-stu-id="b066e-162">The data source name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="b066e-163">After starting the data source name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span><span class="sxs-lookup"><span data-stu-id="b066e-163">After starting the data source name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span> <span data-ttu-id="b066e-164">See [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx) for details.</span><span class="sxs-lookup"><span data-stu-id="b066e-164">See [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx) for details.</span></span>

<span data-ttu-id="b066e-165">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-165">The `api-version` is required.</span></span> <span data-ttu-id="b066e-166">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-166">The current version is `2015-02-28`.</span></span>

<span data-ttu-id="b066e-167">**Request Headers**</span><span class="sxs-lookup"><span data-stu-id="b066e-167">**Request Headers**</span></span>

<span data-ttu-id="b066e-168">The following list describes the required and optional request headers.</span><span class="sxs-lookup"><span data-stu-id="b066e-168">The following list describes the required and optional request headers.</span></span> 

* <span data-ttu-id="b066e-169">`Content-Type`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-169">`Content-Type`: Required.</span></span> <span data-ttu-id="b066e-170">Set this to `application/json`</span><span class="sxs-lookup"><span data-stu-id="b066e-170">Set this to `application/json`</span></span>
* <span data-ttu-id="b066e-171">`api-key`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-171">`api-key`: Required.</span></span> <span data-ttu-id="b066e-172">The `api-key` is used to authenticate the request to your Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-172">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="b066e-173">It is a string value, unique to your service.</span><span class="sxs-lookup"><span data-stu-id="b066e-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="b066e-174">The **Create Data Source** request must include an `api-key` header set to your admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-174">The **Create Data Source** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span> 

<span data-ttu-id="b066e-175">You will also need the service name to construct the request URL.</span><span class="sxs-lookup"><span data-stu-id="b066e-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="b066e-176">You can get both the service name and `api-key` from your service dashboard in the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b066e-176">You can get both the service name and `api-key` from your service dashboard in the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b066e-177">See [Create a Search service in the portal](search-create-service-portal.md) for page navigation help.</span><span class="sxs-lookup"><span data-stu-id="b066e-177">See [Create a Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<a name="CreateDataSourceRequestSyntax"></a>
<span data-ttu-id="b066e-178">**Request Body Syntax**</span><span class="sxs-lookup"><span data-stu-id="b066e-178">**Request Body Syntax**</span></span>

<span data-ttu-id="b066e-179">The body of the request contains a data source definition, which includes type of the data source, credentials to read the data, as well as an optional data change detection and data deletion detection policies that are used to efficiently identify changed or deleted data in the data source when used with a periodically scheduled indexer.</span><span class="sxs-lookup"><span data-stu-id="b066e-179">The body of the request contains a data source definition, which includes type of the data source, credentials to read the data, as well as an optional data change detection and data deletion detection policies that are used to efficiently identify changed or deleted data in the data source when used with a periodically scheduled indexer.</span></span> 

<span data-ttu-id="b066e-180">The syntax for structuring the request payload is as follows.</span><span class="sxs-lookup"><span data-stu-id="b066e-180">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="b066e-181">A sample request is provided further on in this topic.</span><span class="sxs-lookup"><span data-stu-id="b066e-181">A sample request is provided further on in this topic.</span></span>

    { 
        "name" : "Required for POST, optional for PUT. The name of the data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. The name of the table, collection, or blob container you wish to index" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

<span data-ttu-id="b066e-182">Request contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="b066e-182">Request contains the following properties:</span></span> 

* <span data-ttu-id="b066e-183">`name`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-183">`name`: Required.</span></span> <span data-ttu-id="b066e-184">The name of the data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-184">The name of the data source.</span></span> <span data-ttu-id="b066e-185">A data source name must only contain lowercase letters, digits or dashes, cannot start or end with dashes and is limited to 128 characters.</span><span class="sxs-lookup"><span data-stu-id="b066e-185">A data source name must only contain lowercase letters, digits or dashes, cannot start or end with dashes and is limited to 128 characters.</span></span>
* <span data-ttu-id="b066e-186">`description`: An optional description.</span><span class="sxs-lookup"><span data-stu-id="b066e-186">`description`: An optional description.</span></span> 
* <span data-ttu-id="b066e-187">`type`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-187">`type`: Required.</span></span> <span data-ttu-id="b066e-188">Must be one of the supported data source types:</span><span class="sxs-lookup"><span data-stu-id="b066e-188">Must be one of the supported data source types:</span></span>
  * <span data-ttu-id="b066e-189">`azuresql` - Azure SQL Database or SQL Server on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="b066e-189">`azuresql` - Azure SQL Database or SQL Server on Azure VMs</span></span>
  * <span data-ttu-id="b066e-190">`documentdb` - Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b066e-190">`documentdb` - Azure DocumentDB</span></span>
  * <span data-ttu-id="b066e-191">`azureblob` - Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b066e-191">`azureblob` - Azure Blob Storage</span></span>
  * <span data-ttu-id="b066e-192">`azuretable` - Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="b066e-192">`azuretable` - Azure Table Storage</span></span>
* <span data-ttu-id="b066e-193">`credentials`:</span><span class="sxs-lookup"><span data-stu-id="b066e-193">`credentials`:</span></span>
  * <span data-ttu-id="b066e-194">The required `connectionString` property specifies the connection string for the data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-194">The required `connectionString` property specifies the connection string for the data source.</span></span> <span data-ttu-id="b066e-195">The format of the connection string depends on the data source type:</span><span class="sxs-lookup"><span data-stu-id="b066e-195">The format of the connection string depends on the data source type:</span></span> 
    * <span data-ttu-id="b066e-196">For Azure SQL, this is the usual SQL Server connection string.</span><span class="sxs-lookup"><span data-stu-id="b066e-196">For Azure SQL, this is the usual SQL Server connection string.</span></span> <span data-ttu-id="b066e-197">If you're using the Azure portal to retrieve the connection string, use the `ADO.NET connection string` option.</span><span class="sxs-lookup"><span data-stu-id="b066e-197">If you're using the Azure portal to retrieve the connection string, use the `ADO.NET connection string` option.</span></span>
    * <span data-ttu-id="b066e-198">For DocumentDB, the connection string must be in the following format: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`.</span><span class="sxs-lookup"><span data-stu-id="b066e-198">For DocumentDB, the connection string must be in the following format: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`.</span></span> <span data-ttu-id="b066e-199">All of the values are required.</span><span class="sxs-lookup"><span data-stu-id="b066e-199">All of the values are required.</span></span> <span data-ttu-id="b066e-200">You can find them in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b066e-200">You can find them in the [Azure portal](https://portal.azure.com/).</span></span>  
    * <span data-ttu-id="b066e-201">For Azure Blob and Table Storage, this is the storage account connection string.</span><span class="sxs-lookup"><span data-stu-id="b066e-201">For Azure Blob and Table Storage, this is the storage account connection string.</span></span> <span data-ttu-id="b066e-202">The format is described [here](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/).</span><span class="sxs-lookup"><span data-stu-id="b066e-202">The format is described [here](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/).</span></span> <span data-ttu-id="b066e-203">HTTPS endpoint protocol is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-203">HTTPS endpoint protocol is required.</span></span>  
* <span data-ttu-id="b066e-204">`container`, required: specifies the data to index using the `name` and `query` properties:</span><span class="sxs-lookup"><span data-stu-id="b066e-204">`container`, required: specifies the data to index using the `name` and `query` properties:</span></span> 
  * <span data-ttu-id="b066e-205">`name`, required:</span><span class="sxs-lookup"><span data-stu-id="b066e-205">`name`, required:</span></span>
    * <span data-ttu-id="b066e-206">Azure SQL: specifies the table or view.</span><span class="sxs-lookup"><span data-stu-id="b066e-206">Azure SQL: specifies the table or view.</span></span> <span data-ttu-id="b066e-207">You can use schema-qualified names, such as `[dbo].[mytable]`.</span><span class="sxs-lookup"><span data-stu-id="b066e-207">You can use schema-qualified names, such as `[dbo].[mytable]`.</span></span>
    * <span data-ttu-id="b066e-208">DocumentDB: specifies the collection.</span><span class="sxs-lookup"><span data-stu-id="b066e-208">DocumentDB: specifies the collection.</span></span> 
    * <span data-ttu-id="b066e-209">Azure Blob Storage: specifies the storage container.</span><span class="sxs-lookup"><span data-stu-id="b066e-209">Azure Blob Storage: specifies the storage container.</span></span>
    * <span data-ttu-id="b066e-210">Azure Table Storage: specifies the name of the table.</span><span class="sxs-lookup"><span data-stu-id="b066e-210">Azure Table Storage: specifies the name of the table.</span></span> 
  * <span data-ttu-id="b066e-211">`query`, optional:</span><span class="sxs-lookup"><span data-stu-id="b066e-211">`query`, optional:</span></span>
    * <span data-ttu-id="b066e-212">DocumentDB: allows you to specify a query that flattens an arbitrary JSON document layout into a flat schema that Azure Search can index.</span><span class="sxs-lookup"><span data-stu-id="b066e-212">DocumentDB: allows you to specify a query that flattens an arbitrary JSON document layout into a flat schema that Azure Search can index.</span></span>  
    * <span data-ttu-id="b066e-213">Azure Blob Storage: allows you to specify a virtual folder within the blob container.</span><span class="sxs-lookup"><span data-stu-id="b066e-213">Azure Blob Storage: allows you to specify a virtual folder within the blob container.</span></span> <span data-ttu-id="b066e-214">For example, for blob path `mycontainer/documents/blob.pdf`, `documents` can be used as the virtual folder.</span><span class="sxs-lookup"><span data-stu-id="b066e-214">For example, for blob path `mycontainer/documents/blob.pdf`, `documents` can be used as the virtual folder.</span></span>
    * <span data-ttu-id="b066e-215">Azure Table Storage: allows you to specify a query that filters the set of rows to be imported.</span><span class="sxs-lookup"><span data-stu-id="b066e-215">Azure Table Storage: allows you to specify a query that filters the set of rows to be imported.</span></span>
    * <span data-ttu-id="b066e-216">Azure SQL: query is not supported.</span><span class="sxs-lookup"><span data-stu-id="b066e-216">Azure SQL: query is not supported.</span></span> <span data-ttu-id="b066e-217">If you need this functionality, please vote for [this suggestion](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)</span><span class="sxs-lookup"><span data-stu-id="b066e-217">If you need this functionality, please vote for [this suggestion](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)</span></span>
* <span data-ttu-id="b066e-218">The optional `dataChangeDetectionPolicy` and `dataDeletionDetectionPolicy` properties are described below.</span><span class="sxs-lookup"><span data-stu-id="b066e-218">The optional `dataChangeDetectionPolicy` and `dataDeletionDetectionPolicy` properties are described below.</span></span>

<a name="DataChangeDetectionPolicies"></a>
<span data-ttu-id="b066e-219">**Data Change Detection Policies**</span><span class="sxs-lookup"><span data-stu-id="b066e-219">**Data Change Detection Policies**</span></span>

<span data-ttu-id="b066e-220">The purpose of a data change detection policy is to efficiently identify changed data items.</span><span class="sxs-lookup"><span data-stu-id="b066e-220">The purpose of a data change detection policy is to efficiently identify changed data items.</span></span> <span data-ttu-id="b066e-221">Supported policies vary based on the data source type.</span><span class="sxs-lookup"><span data-stu-id="b066e-221">Supported policies vary based on the data source type.</span></span> <span data-ttu-id="b066e-222">Sections below describe each policy.</span><span class="sxs-lookup"><span data-stu-id="b066e-222">Sections below describe each policy.</span></span> 

<span data-ttu-id="b066e-223">***High Watermark Change Detection Policy***</span><span class="sxs-lookup"><span data-stu-id="b066e-223">***High Watermark Change Detection Policy***</span></span> 

<span data-ttu-id="b066e-224">Use this policy when your data source contains a column or property that meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="b066e-224">Use this policy when your data source contains a column or property that meets the following criteria:</span></span>

* <span data-ttu-id="b066e-225">All inserts specify a value for the column.</span><span class="sxs-lookup"><span data-stu-id="b066e-225">All inserts specify a value for the column.</span></span> 
* <span data-ttu-id="b066e-226">All updates to an item also change the value of the column.</span><span class="sxs-lookup"><span data-stu-id="b066e-226">All updates to an item also change the value of the column.</span></span> 
* <span data-ttu-id="b066e-227">The value of this column increases with each change.</span><span class="sxs-lookup"><span data-stu-id="b066e-227">The value of this column increases with each change.</span></span>
* <span data-ttu-id="b066e-228">Queries that use a filter clause similar to the following `WHERE [High Water Mark Column] > [Current High Water Mark Value]` can be executed efficiently.</span><span class="sxs-lookup"><span data-stu-id="b066e-228">Queries that use a filter clause similar to the following `WHERE [High Water Mark Column] > [Current High Water Mark Value]` can be executed efficiently.</span></span>

<span data-ttu-id="b066e-229">For example, when using Azure SQL data sources, an indexed `rowversion` column is the ideal candidate for use with with the high water mark policy.</span><span class="sxs-lookup"><span data-stu-id="b066e-229">For example, when using Azure SQL data sources, an indexed `rowversion` column is the ideal candidate for use with with the high water mark policy.</span></span> 

<span data-ttu-id="b066e-230">This policy can be specified as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-230">This policy can be specified as follows:</span></span>

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

<span data-ttu-id="b066e-231">When using DocumentDB data sources, you must use the `_ts` property provided by DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b066e-231">When using DocumentDB data sources, you must use the `_ts` property provided by DocumentDB.</span></span> 

<span data-ttu-id="b066e-232">When using Azure Blob data sources, Azure Search automatically uses a high watermark change detection policy based on a blob's last-modified timestamp; you don't need to specify such a policy yourself.</span><span class="sxs-lookup"><span data-stu-id="b066e-232">When using Azure Blob data sources, Azure Search automatically uses a high watermark change detection policy based on a blob's last-modified timestamp; you don't need to specify such a policy yourself.</span></span>   

<span data-ttu-id="b066e-233">***SQL Integrated Change Detection Policy***</span><span class="sxs-lookup"><span data-stu-id="b066e-233">***SQL Integrated Change Detection Policy***</span></span>

<span data-ttu-id="b066e-234">If your SQL database supports [change tracking](https://msdn.microsoft.com/library/bb933875.aspx), we recommend using SQL Integrated Change Tracking Policy.</span><span class="sxs-lookup"><span data-stu-id="b066e-234">If your SQL database supports [change tracking](https://msdn.microsoft.com/library/bb933875.aspx), we recommend using SQL Integrated Change Tracking Policy.</span></span> <span data-ttu-id="b066e-235">This policy enables the most efficient change tracking, and allows Azure Search to identify deleted rows without you having to have an explicit "soft delete" column in your schema.</span><span class="sxs-lookup"><span data-stu-id="b066e-235">This policy enables the most efficient change tracking, and allows Azure Search to identify deleted rows without you having to have an explicit "soft delete" column in your schema.</span></span>

<span data-ttu-id="b066e-236">Integrated change tracking is supported starting with the following SQL Server database versions:</span><span class="sxs-lookup"><span data-stu-id="b066e-236">Integrated change tracking is supported starting with the following SQL Server database versions:</span></span> 

* <span data-ttu-id="b066e-237">SQL Server 2008 R2, if you're using SQL Server on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="b066e-237">SQL Server 2008 R2, if you're using SQL Server on Azure VMs.</span></span>
* <span data-ttu-id="b066e-238">Azure SQL Database V12, if you're using Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b066e-238">Azure SQL Database V12, if you're using Azure SQL Database.</span></span>  

<span data-ttu-id="b066e-239">When using SQL Integrated Change Tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span><span class="sxs-lookup"><span data-stu-id="b066e-239">When using SQL Integrated Change Tracking policy, do not specify a separate data deletion detection policy - this policy has built-in support for identifying deleted rows.</span></span> 

<span data-ttu-id="b066e-240">This policy can only be used with tables; it cannot be used with views.</span><span class="sxs-lookup"><span data-stu-id="b066e-240">This policy can only be used with tables; it cannot be used with views.</span></span> <span data-ttu-id="b066e-241">You need to enable change tracking for the table you're using before you can use this policy.</span><span class="sxs-lookup"><span data-stu-id="b066e-241">You need to enable change tracking for the table you're using before you can use this policy.</span></span> <span data-ttu-id="b066e-242">See [Enable and disable change tracking](https://msdn.microsoft.com/library/bb964713.aspx) for instructions.</span><span class="sxs-lookup"><span data-stu-id="b066e-242">See [Enable and disable change tracking](https://msdn.microsoft.com/library/bb964713.aspx) for instructions.</span></span>    

<span data-ttu-id="b066e-243">When structuring the **Create Data Source** request, SQL integrated change tracking policy can be specified as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-243">When structuring the **Create Data Source** request, SQL integrated change tracking policy can be specified as follows:</span></span>

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
<span data-ttu-id="b066e-244">**Data Deletion Detection Policies**</span><span class="sxs-lookup"><span data-stu-id="b066e-244">**Data Deletion Detection Policies**</span></span>

<span data-ttu-id="b066e-245">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span><span class="sxs-lookup"><span data-stu-id="b066e-245">The purpose of a data deletion detection policy is to efficiently identify deleted data items.</span></span> <span data-ttu-id="b066e-246">Currently, the only supported policy is the `Soft Delete` policy, which allows identifying deleted items based on the value of a `soft delete` column or property in the data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-246">Currently, the only supported policy is the `Soft Delete` policy, which allows identifying deleted items based on the value of a `soft delete` column or property in the data source.</span></span> <span data-ttu-id="b066e-247">This policy can be specified as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-247">This policy can be specified as follows:</span></span>

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "the column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "the value that identifies a row as deleted" 
    }

> [!NOTE]
> <span data-ttu-id="b066e-248">Only columns with string, integer, or Boolean values are supported.</span><span class="sxs-lookup"><span data-stu-id="b066e-248">Only columns with string, integer, or Boolean values are supported.</span></span> <span data-ttu-id="b066e-249">The value used as `softDeleteMarkerValue` must be a string, even if the corresponding column holds integers or booleans.</span><span class="sxs-lookup"><span data-stu-id="b066e-249">The value used as `softDeleteMarkerValue` must be a string, even if the corresponding column holds integers or booleans.</span></span> <span data-ttu-id="b066e-250">For example, if the value that appears in your data source is 1, use `"1"` as the `softDeleteMarkerValue`.</span><span class="sxs-lookup"><span data-stu-id="b066e-250">For example, if the value that appears in your data source is 1, use `"1"` as the `softDeleteMarkerValue`.</span></span>    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
<span data-ttu-id="b066e-251">**Request Body Examples**</span><span class="sxs-lookup"><span data-stu-id="b066e-251">**Request Body Examples**</span></span>

<span data-ttu-id="b066e-252">If you intend to use the data source with an indexer that runs on a schedule, this example shows how to specify change and deletion detection policies:</span><span class="sxs-lookup"><span data-stu-id="b066e-252">If you intend to use the data source with an indexer that runs on a schedule, this example shows how to specify change and deletion detection policies:</span></span> 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

<span data-ttu-id="b066e-253">If you only intend to use the data source for one-time copy of the data, the policies can be omitted:</span><span class="sxs-lookup"><span data-stu-id="b066e-253">If you only intend to use the data source for one-time copy of the data, the policies can be omitted:</span></span>

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

<span data-ttu-id="b066e-254">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-254">**Response**</span></span>

<span data-ttu-id="b066e-255">For a successful request: 201 Created.</span><span class="sxs-lookup"><span data-stu-id="b066e-255">For a successful request: 201 Created.</span></span> 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a><span data-ttu-id="b066e-256">Update Data Source</span><span class="sxs-lookup"><span data-stu-id="b066e-256">Update Data Source</span></span>
<span data-ttu-id="b066e-257">You can update an existing data source using an HTTP PUT request.</span><span class="sxs-lookup"><span data-stu-id="b066e-257">You can update an existing data source using an HTTP PUT request.</span></span> <span data-ttu-id="b066e-258">You specify the name of the data source to update on the request URI:</span><span class="sxs-lookup"><span data-stu-id="b066e-258">You specify the name of the data source to update on the request URI:</span></span>

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="b066e-259">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-259">The `api-version` is required.</span></span> <span data-ttu-id="b066e-260">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-260">The current version is `2015-02-28`.</span></span> <span data-ttu-id="b066e-261">[Azure Search API versions](https://msdn.microsoft.com/library/azure/dn864560.aspx) has details and more information about alternative versions.</span><span class="sxs-lookup"><span data-stu-id="b066e-261">[Azure Search API versions](https://msdn.microsoft.com/library/azure/dn864560.aspx) has details and more information about alternative versions.</span></span>

<span data-ttu-id="b066e-262">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-262">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-263">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-263">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-264">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-264">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-265">**Request**</span><span class="sxs-lookup"><span data-stu-id="b066e-265">**Request**</span></span>

<span data-ttu-id="b066e-266">The request body syntax is the same as for [Create Data Source requests](#CreateDataSourceRequestSyntax).</span><span class="sxs-lookup"><span data-stu-id="b066e-266">The request body syntax is the same as for [Create Data Source requests](#CreateDataSourceRequestSyntax).</span></span>

<span data-ttu-id="b066e-267">Some properties cannot be updated on an existing data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-267">Some properties cannot be updated on an existing data source.</span></span> <span data-ttu-id="b066e-268">For example, you cannot change the type of an existing data source.</span><span class="sxs-lookup"><span data-stu-id="b066e-268">For example, you cannot change the type of an existing data source.</span></span>  

<span data-ttu-id="b066e-269">If you don't want to change the connection string for an existing data source, you can specify the literal `<unchanged>` for the connection string.</span><span class="sxs-lookup"><span data-stu-id="b066e-269">If you don't want to change the connection string for an existing data source, you can specify the literal `<unchanged>` for the connection string.</span></span> <span data-ttu-id="b066e-270">This is helpful in situations where you need to update a data source but don't have convenient access to the connection string since it is security-sensitive data.</span><span class="sxs-lookup"><span data-stu-id="b066e-270">This is helpful in situations where you need to update a data source but don't have convenient access to the connection string since it is security-sensitive data.</span></span>

<span data-ttu-id="b066e-271">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-271">**Response**</span></span>

<span data-ttu-id="b066e-272">For a successful request: 201 Created if a new data source was created, and 204 No Content if an existing data source was updated.</span><span class="sxs-lookup"><span data-stu-id="b066e-272">For a successful request: 201 Created if a new data source was created, and 204 No Content if an existing data source was updated.</span></span>

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a><span data-ttu-id="b066e-273">List Data Sources</span><span class="sxs-lookup"><span data-stu-id="b066e-273">List Data Sources</span></span>
<span data-ttu-id="b066e-274">The **List Data Sources** operation returns a list of the data sources in your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-274">The **List Data Sources** operation returns a list of the data sources in your Azure Search service.</span></span> 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-275">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-275">The `api-version` is required.</span></span> <span data-ttu-id="b066e-276">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-276">The current version is `2015-02-28`.</span></span> 

<span data-ttu-id="b066e-277">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-277">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-278">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-278">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-279">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-279">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-280">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-280">**Response**</span></span>

<span data-ttu-id="b066e-281">For a successful request: 200 OK.</span><span class="sxs-lookup"><span data-stu-id="b066e-281">For a successful request: 200 OK.</span></span>

<span data-ttu-id="b066e-282">Here is an example response body:</span><span class="sxs-lookup"><span data-stu-id="b066e-282">Here is an example response body:</span></span>

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

<span data-ttu-id="b066e-283">Note that you can filter the response down to just the properties you're interested in.</span><span class="sxs-lookup"><span data-stu-id="b066e-283">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="b066e-284">For example, if you want only a list of data source names, use the OData `$select` query option:</span><span class="sxs-lookup"><span data-stu-id="b066e-284">For example, if you want only a list of data source names, use the OData `$select` query option:</span></span>

    GET /datasources?api-version=205-02-28&$select=name

<span data-ttu-id="b066e-285">In this case, the response from the above example would appear as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-285">In this case, the response from the above example would appear as follows:</span></span> 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

<span data-ttu-id="b066e-286">This is a useful technique to save bandwidth if you have a lot of data sources in your Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-286">This is a useful technique to save bandwidth if you have a lot of data sources in your Search service.</span></span>

<a name="GetDataSource"></a>

## <a name="get-data-source"></a><span data-ttu-id="b066e-287">Get Data Source</span><span class="sxs-lookup"><span data-stu-id="b066e-287">Get Data Source</span></span>
<span data-ttu-id="b066e-288">The **Get Data Source** operation gets the data source definition from Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b066e-288">The **Get Data Source** operation gets the data source definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-289">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-289">The `api-version` is required.</span></span> <span data-ttu-id="b066e-290">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-290">The current version is `2015-02-28`.</span></span> 

<span data-ttu-id="b066e-291">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-291">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-292">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-292">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-293">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-293">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-294">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-294">**Response**</span></span>

<span data-ttu-id="b066e-295">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-295">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="b066e-296">The response is similar to examples in [Create Data Source example requests](#CreateDataSourceRequestExamples):</span><span class="sxs-lookup"><span data-stu-id="b066e-296">The response is similar to examples in [Create Data Source example requests](#CreateDataSourceRequestExamples):</span></span> 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> <span data-ttu-id="b066e-297">Do not set the `Accept` request header to `application/json;odata.metadata=none` when calling this API as doing so will cause `@odata.type` attribute to be omitted from the response and you won't be able to differentiate between data change and data deletion detection policies of different types.</span><span class="sxs-lookup"><span data-stu-id="b066e-297">Do not set the `Accept` request header to `application/json;odata.metadata=none` when calling this API as doing so will cause `@odata.type` attribute to be omitted from the response and you won't be able to differentiate between data change and data deletion detection policies of different types.</span></span> 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a><span data-ttu-id="b066e-298">Delete Data Source</span><span class="sxs-lookup"><span data-stu-id="b066e-298">Delete Data Source</span></span>
<span data-ttu-id="b066e-299">The **Delete Data Source** operation removes a data source from your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-299">The **Delete Data Source** operation removes a data source from your Azure Search service.</span></span>

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="b066e-300">If any indexers reference the data source that you're deleting, the delete operation will still proceed.</span><span class="sxs-lookup"><span data-stu-id="b066e-300">If any indexers reference the data source that you're deleting, the delete operation will still proceed.</span></span> <span data-ttu-id="b066e-301">However, those indexers will transition into an error state upon their next run.</span><span class="sxs-lookup"><span data-stu-id="b066e-301">However, those indexers will transition into an error state upon their next run.</span></span>  
> 
> 

<span data-ttu-id="b066e-302">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-302">The `api-version` is required.</span></span> <span data-ttu-id="b066e-303">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-303">The current version is `2015-02-28`.</span></span> 

<span data-ttu-id="b066e-304">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-304">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-305">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-305">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-306">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-306">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-307">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-307">**Response**</span></span>

<span data-ttu-id="b066e-308">Status Code: 204 No Content is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-308">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a><span data-ttu-id="b066e-309">Create Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-309">Create Indexer</span></span>
<span data-ttu-id="b066e-310">You can create a new indexer within an Azure Search service using an HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="b066e-310">You can create a new indexer within an Azure Search service using an HTTP POST request.</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="b066e-311">Alternatively, you can use PUT and specify the data source name on the URI.</span><span class="sxs-lookup"><span data-stu-id="b066e-311">Alternatively, you can use PUT and specify the data source name on the URI.</span></span> <span data-ttu-id="b066e-312">If the data source does not exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="b066e-312">If the data source does not exist, it will be created.</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> <span data-ttu-id="b066e-313">The maximum number of indexers allowed varies by pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b066e-313">The maximum number of indexers allowed varies by pricing tier.</span></span> <span data-ttu-id="b066e-314">The free service allows up to 3 indexers.</span><span class="sxs-lookup"><span data-stu-id="b066e-314">The free service allows up to 3 indexers.</span></span> <span data-ttu-id="b066e-315">Standard service allows 50 indexers.</span><span class="sxs-lookup"><span data-stu-id="b066e-315">Standard service allows 50 indexers.</span></span> <span data-ttu-id="b066e-316">See [Service Limits](search-limits-quotas-capacity.md) for details.</span><span class="sxs-lookup"><span data-stu-id="b066e-316">See [Service Limits](search-limits-quotas-capacity.md) for details.</span></span>
> 
> 

<span data-ttu-id="b066e-317">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-317">The `api-version` is required.</span></span> <span data-ttu-id="b066e-318">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-318">The current version is `2015-02-28`.</span></span> 

<span data-ttu-id="b066e-319">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-319">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-320">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-320">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-321">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-321">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<a name="CreateIndexerRequestSyntax"></a>
<span data-ttu-id="b066e-322">**Request Body Syntax**</span><span class="sxs-lookup"><span data-stu-id="b066e-322">**Request Body Syntax**</span></span>

<span data-ttu-id="b066e-323">The body of the request contains an indexer definition, which specifies the data source and the target index for indexing, as well as optional indexing schedule and parameters.</span><span class="sxs-lookup"><span data-stu-id="b066e-323">The body of the request contains an indexer definition, which specifies the data source and the target index for indexing, as well as optional indexing schedule and parameters.</span></span> 

<span data-ttu-id="b066e-324">The syntax for structuring the request payload is as follows.</span><span class="sxs-lookup"><span data-stu-id="b066e-324">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="b066e-325">A sample request is provided further on in this topic.</span><span class="sxs-lookup"><span data-stu-id="b066e-325">A sample request is provided further on in this topic.</span></span>

    { 
        "name" : "Required for POST, optional for PUT. The name of the indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. The name of an existing data source",
        "targetIndexName" : "Required. The name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether the indexer is disabled. False by default.  
    }

<span data-ttu-id="b066e-326">**Indexer Schedule**</span><span class="sxs-lookup"><span data-stu-id="b066e-326">**Indexer Schedule**</span></span>

<span data-ttu-id="b066e-327">An indexer can optionally specify a schedule.</span><span class="sxs-lookup"><span data-stu-id="b066e-327">An indexer can optionally specify a schedule.</span></span> <span data-ttu-id="b066e-328">If a schedule is present, the indexer will run periodically as per schedule.</span><span class="sxs-lookup"><span data-stu-id="b066e-328">If a schedule is present, the indexer will run periodically as per schedule.</span></span> <span data-ttu-id="b066e-329">Schedule has the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b066e-329">Schedule has the following attributes:</span></span>

* <span data-ttu-id="b066e-330">`interval`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-330">`interval`: Required.</span></span> <span data-ttu-id="b066e-331">A duration value that specifies an interval or period for indexer runs.</span><span class="sxs-lookup"><span data-stu-id="b066e-331">A duration value that specifies an interval or period for indexer runs.</span></span> <span data-ttu-id="b066e-332">The smallest allowed interval is 5 minutes; the longest is one day.</span><span class="sxs-lookup"><span data-stu-id="b066e-332">The smallest allowed interval is 5 minutes; the longest is one day.</span></span> <span data-ttu-id="b066e-333">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span><span class="sxs-lookup"><span data-stu-id="b066e-333">It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an [ISO 8601 duration](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) value).</span></span> <span data-ttu-id="b066e-334">The pattern for this is: `"P[nD][T[nH][nM]]"`.</span><span class="sxs-lookup"><span data-stu-id="b066e-334">The pattern for this is: `"P[nD][T[nH][nM]]"`.</span></span> <span data-ttu-id="b066e-335">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span><span class="sxs-lookup"><span data-stu-id="b066e-335">Examples: `PT15M` for every 15 minutes, `PT2H` for every 2 hours.</span></span> 
* <span data-ttu-id="b066e-336">`startTime`: Required.</span><span class="sxs-lookup"><span data-stu-id="b066e-336">`startTime`: Required.</span></span> <span data-ttu-id="b066e-337">An UTC datetime when the indexer should start running.</span><span class="sxs-lookup"><span data-stu-id="b066e-337">An UTC datetime when the indexer should start running.</span></span> 

<span data-ttu-id="b066e-338">**Indexer Parameters**</span><span class="sxs-lookup"><span data-stu-id="b066e-338">**Indexer Parameters**</span></span>

<span data-ttu-id="b066e-339">An indexer can optionally specify several parameters that affect its behavior.</span><span class="sxs-lookup"><span data-stu-id="b066e-339">An indexer can optionally specify several parameters that affect its behavior.</span></span> <span data-ttu-id="b066e-340">All of the parameters are optional.</span><span class="sxs-lookup"><span data-stu-id="b066e-340">All of the parameters are optional.</span></span>  

* <span data-ttu-id="b066e-341">`maxFailedItems` : The number of items that can fail to be indexed before an indexer run is considered a failure.</span><span class="sxs-lookup"><span data-stu-id="b066e-341">`maxFailedItems` : The number of items that can fail to be indexed before an indexer run is considered a failure.</span></span> <span data-ttu-id="b066e-342">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="b066e-342">Default is 0.</span></span> <span data-ttu-id="b066e-343">Information about failed items is returned by the [Get Indexer Status](#GetIndexerStatus) operation.</span><span class="sxs-lookup"><span data-stu-id="b066e-343">Information about failed items is returned by the [Get Indexer Status](#GetIndexerStatus) operation.</span></span> 
* <span data-ttu-id="b066e-344">`maxFailedItemsPerBatch` : The number of items that can fail to be indexed in each batch before an indexer run is considered a failure.</span><span class="sxs-lookup"><span data-stu-id="b066e-344">`maxFailedItemsPerBatch` : The number of items that can fail to be indexed in each batch before an indexer run is considered a failure.</span></span> <span data-ttu-id="b066e-345">Default is 0.</span><span class="sxs-lookup"><span data-stu-id="b066e-345">Default is 0.</span></span>
* <span data-ttu-id="b066e-346">`base64EncodeKeys`: Specifies whether or not document keys will be base-64 encoded.</span><span class="sxs-lookup"><span data-stu-id="b066e-346">`base64EncodeKeys`: Specifies whether or not document keys will be base-64 encoded.</span></span> <span data-ttu-id="b066e-347">Azure Search imposes restrictions on characters that can be present in a document key.</span><span class="sxs-lookup"><span data-stu-id="b066e-347">Azure Search imposes restrictions on characters that can be present in a document key.</span></span> <span data-ttu-id="b066e-348">However, the values in your source data may contain characters that are invalid.</span><span class="sxs-lookup"><span data-stu-id="b066e-348">However, the values in your source data may contain characters that are invalid.</span></span> <span data-ttu-id="b066e-349">If it is necessary to index such values as document keys, this flag can be set to true.</span><span class="sxs-lookup"><span data-stu-id="b066e-349">If it is necessary to index such values as document keys, this flag can be set to true.</span></span> <span data-ttu-id="b066e-350">Default is `false`.</span><span class="sxs-lookup"><span data-stu-id="b066e-350">Default is `false`.</span></span>
* <span data-ttu-id="b066e-351">`batchSize`: Specifies the number of items that are read from the data source and indexed as a single batch in order to improve performance.</span><span class="sxs-lookup"><span data-stu-id="b066e-351">`batchSize`: Specifies the number of items that are read from the data source and indexed as a single batch in order to improve performance.</span></span> <span data-ttu-id="b066e-352">The default depends on the data source type: it is 1000 for  Azure SQL and DocumentDB, and 10 for Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b066e-352">The default depends on the data source type: it is 1000 for  Azure SQL and DocumentDB, and 10 for Azure Blob Storage.</span></span>

<span data-ttu-id="b066e-353">**Field Mappings**</span><span class="sxs-lookup"><span data-stu-id="b066e-353">**Field Mappings**</span></span>

<span data-ttu-id="b066e-354">You can use field mappings to map a field name in the data source to a different field name in the target index.</span><span class="sxs-lookup"><span data-stu-id="b066e-354">You can use field mappings to map a field name in the data source to a different field name in the target index.</span></span> <span data-ttu-id="b066e-355">For example, consider a source table with a field `_id`.</span><span class="sxs-lookup"><span data-stu-id="b066e-355">For example, consider a source table with a field `_id`.</span></span> <span data-ttu-id="b066e-356">Azure Search doesn't allow a field name starting with an underscore, so the field must be renamed.</span><span class="sxs-lookup"><span data-stu-id="b066e-356">Azure Search doesn't allow a field name starting with an underscore, so the field must be renamed.</span></span> <span data-ttu-id="b066e-357">This can be done using the `fieldMappings` property of the indexer as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-357">This can be done using the `fieldMappings` property of the indexer as follows:</span></span> 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

<span data-ttu-id="b066e-358">You can specify multiple field mappings:</span><span class="sxs-lookup"><span data-stu-id="b066e-358">You can specify multiple field mappings:</span></span> 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

<span data-ttu-id="b066e-359">Both source and target field names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="b066e-359">Both source and target field names are case-insensitive.</span></span>

<a name="FieldMappingFunctions"></a>
<span data-ttu-id="b066e-360">***Field Mapping Functions***</span><span class="sxs-lookup"><span data-stu-id="b066e-360">***Field Mapping Functions***</span></span>

<span data-ttu-id="b066e-361">Field mappings can also be used to transform source field values using *mapping functions*.</span><span class="sxs-lookup"><span data-stu-id="b066e-361">Field mappings can also be used to transform source field values using *mapping functions*.</span></span>

<span data-ttu-id="b066e-362">Only one such function is currently supported: `jsonArrayToStringCollection`.</span><span class="sxs-lookup"><span data-stu-id="b066e-362">Only one such function is currently supported: `jsonArrayToStringCollection`.</span></span> <span data-ttu-id="b066e-363">It parses a field that contains a string formatted as a JSON array into a Collection(Edm.String) field in the target index.</span><span class="sxs-lookup"><span data-stu-id="b066e-363">It parses a field that contains a string formatted as a JSON array into a Collection(Edm.String) field in the target index.</span></span> <span data-ttu-id="b066e-364">It is intended for use with Azure SQL indexer in particular, since SQL doesn't have a native collection data type.</span><span class="sxs-lookup"><span data-stu-id="b066e-364">It is intended for use with Azure SQL indexer in particular, since SQL doesn't have a native collection data type.</span></span> <span data-ttu-id="b066e-365">It can be used as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-365">It can be used as follows:</span></span> 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

<span data-ttu-id="b066e-366">For example, if the source field contains the string `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `"red"`, `"white"` and `"blue"`.</span><span class="sxs-lookup"><span data-stu-id="b066e-366">For example, if the source field contains the string `["red", "white", "blue"]`, then the target field of type `Collection(Edm.String)` will be populated with the three values `"red"`, `"white"` and `"blue"`.</span></span>

<span data-ttu-id="b066e-367">Note that the `targetFieldName` property is optional; if left out, the `sourceFieldName` value is used.</span><span class="sxs-lookup"><span data-stu-id="b066e-367">Note that the `targetFieldName` property is optional; if left out, the `sourceFieldName` value is used.</span></span> 

<a name="CreateIndexerRequestExamples"></a>
<span data-ttu-id="b066e-368">**Request Body Examples**</span><span class="sxs-lookup"><span data-stu-id="b066e-368">**Request Body Examples**</span></span>

<span data-ttu-id="b066e-369">The following example creates an indexer that copies data from the table referenced by the `ordersds` data source to the `orders` index on a schedule that starts on Jan 1, 2015 UTC and runs hourly.</span><span class="sxs-lookup"><span data-stu-id="b066e-369">The following example creates an indexer that copies data from the table referenced by the `ordersds` data source to the `orders` index on a schedule that starts on Jan 1, 2015 UTC and runs hourly.</span></span> <span data-ttu-id="b066e-370">Each indexer invocation will be successful if no more than 5 items fail to be indexed in each batch, and no more than 10 items fail to be indexed in total.</span><span class="sxs-lookup"><span data-stu-id="b066e-370">Each indexer invocation will be successful if no more than 5 items fail to be indexed in each batch, and no more than 10 items fail to be indexed in total.</span></span> 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

<span data-ttu-id="b066e-371">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-371">**Response**</span></span>

<span data-ttu-id="b066e-372">201 Created for a successful request.</span><span class="sxs-lookup"><span data-stu-id="b066e-372">201 Created for a successful request.</span></span>

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a><span data-ttu-id="b066e-373">Update Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-373">Update Indexer</span></span>
<span data-ttu-id="b066e-374">You can update an existing indexer using an HTTP PUT request.</span><span class="sxs-lookup"><span data-stu-id="b066e-374">You can update an existing indexer using an HTTP PUT request.</span></span> <span data-ttu-id="b066e-375">You specify the name of the indexer to update on the request URI:</span><span class="sxs-lookup"><span data-stu-id="b066e-375">You specify the name of the indexer to update on the request URI:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="b066e-376">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-376">The `api-version` is required.</span></span> <span data-ttu-id="b066e-377">The current version is `2015-02-28`.</span><span class="sxs-lookup"><span data-stu-id="b066e-377">The current version is `2015-02-28`.</span></span> 

<span data-ttu-id="b066e-378">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-378">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-379">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-379">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-380">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-380">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-381">**Request**</span><span class="sxs-lookup"><span data-stu-id="b066e-381">**Request**</span></span>

<span data-ttu-id="b066e-382">The request body syntax is the same as for [Create Indexer requests](#CreateIndexerRequestSyntax).</span><span class="sxs-lookup"><span data-stu-id="b066e-382">The request body syntax is the same as for [Create Indexer requests](#CreateIndexerRequestSyntax).</span></span>

<span data-ttu-id="b066e-383">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-383">**Response**</span></span>

<span data-ttu-id="b066e-384">For a successful request: 201 Created if a new indexer was created, and 204 No Content if an existing indexer was updated.</span><span class="sxs-lookup"><span data-stu-id="b066e-384">For a successful request: 201 Created if a new indexer was created, and 204 No Content if an existing indexer was updated.</span></span>

<a name="ListIndexers"></a>

## <a name="list-indexers"></a><span data-ttu-id="b066e-385">List Indexers</span><span class="sxs-lookup"><span data-stu-id="b066e-385">List Indexers</span></span>
<span data-ttu-id="b066e-386">The **List Indexers** operation returns the list of indexers in your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-386">The **List Indexers** operation returns the list of indexers in your Azure Search service.</span></span> 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


<span data-ttu-id="b066e-387">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-387">The `api-version` is required.</span></span> <span data-ttu-id="b066e-388">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-388">The preview version is `2015-02-28-Preview`.</span></span> <span data-ttu-id="b066e-389">[Azure Search versioning](https://msdn.microsoft.com/library/azure/dn864560.aspx) has details and more information about alternative versions.</span><span class="sxs-lookup"><span data-stu-id="b066e-389">[Azure Search versioning](https://msdn.microsoft.com/library/azure/dn864560.aspx) has details and more information about alternative versions.</span></span>

<span data-ttu-id="b066e-390">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-390">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-391">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-391">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-392">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-392">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-393">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-393">**Response**</span></span>

<span data-ttu-id="b066e-394">For a successful request: 200 OK.</span><span class="sxs-lookup"><span data-stu-id="b066e-394">For a successful request: 200 OK.</span></span>

<span data-ttu-id="b066e-395">Here is an example response body:</span><span class="sxs-lookup"><span data-stu-id="b066e-395">Here is an example response body:</span></span>

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

<span data-ttu-id="b066e-396">Note that you can filter the response down to just the properties you're interested in.</span><span class="sxs-lookup"><span data-stu-id="b066e-396">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="b066e-397">For example, if you want only a list of indexer names, use the OData `$select` query option:</span><span class="sxs-lookup"><span data-stu-id="b066e-397">For example, if you want only a list of indexer names, use the OData `$select` query option:</span></span>

    GET /indexers?api-version=2014-10-20-Preview&$select=name

<span data-ttu-id="b066e-398">In this case, the response from the above example would appear as follows:</span><span class="sxs-lookup"><span data-stu-id="b066e-398">In this case, the response from the above example would appear as follows:</span></span> 

    {
      "value" : [ { "name": "myindexer" } ]
    }

<span data-ttu-id="b066e-399">This is a useful technique to save bandwidth if you have a lot of indexers in your Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-399">This is a useful technique to save bandwidth if you have a lot of indexers in your Search service.</span></span>

<a name="GetIndexer"></a>

## <a name="get-indexer"></a><span data-ttu-id="b066e-400">Get Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-400">Get Indexer</span></span>
<span data-ttu-id="b066e-401">The **Get Indexer** operation gets the indexer definition from Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b066e-401">The **Get Indexer** operation gets the indexer definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-402">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-402">The `api-version` is required.</span></span> <span data-ttu-id="b066e-403">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-403">The preview version is `2015-02-28-Preview`.</span></span> 

<span data-ttu-id="b066e-404">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-404">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-405">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-405">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-406">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-406">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-407">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-407">**Response**</span></span>

<span data-ttu-id="b066e-408">Status Code: 200 OK is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-408">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="b066e-409">The response is similar to examples in [Create Indexer example requests](#CreateIndexerRequestExamples):</span><span class="sxs-lookup"><span data-stu-id="b066e-409">The response is similar to examples in [Create Indexer example requests](#CreateIndexerRequestExamples):</span></span> 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a><span data-ttu-id="b066e-410">Delete Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-410">Delete Indexer</span></span>
<span data-ttu-id="b066e-411">The **Delete Indexer** operation removes an indexer from your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="b066e-411">The **Delete Indexer** operation removes an indexer from your Azure Search service.</span></span>

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-412">When an indexer is deleted, the indexer executions in progress at that time will run to completion, but no further executions will be scheduled.</span><span class="sxs-lookup"><span data-stu-id="b066e-412">When an indexer is deleted, the indexer executions in progress at that time will run to completion, but no further executions will be scheduled.</span></span> <span data-ttu-id="b066e-413">Attempts to use a non-existent indexer will result in HTTP status code 404 Not Found.</span><span class="sxs-lookup"><span data-stu-id="b066e-413">Attempts to use a non-existent indexer will result in HTTP status code 404 Not Found.</span></span> 

<span data-ttu-id="b066e-414">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-414">The `api-version` is required.</span></span> <span data-ttu-id="b066e-415">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-415">The preview version is `2015-02-28-Preview`.</span></span> 

<span data-ttu-id="b066e-416">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-416">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-417">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-417">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-418">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-418">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-419">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-419">**Response**</span></span>

<span data-ttu-id="b066e-420">Status Code: 204 No Content is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-420">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="RunIndexer"></a>

## <a name="run-indexer"></a><span data-ttu-id="b066e-421">Run Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-421">Run Indexer</span></span>
<span data-ttu-id="b066e-422">In addition to running periodically on a schedule, an indexer can also be invoked on demand via the **Run Indexer** operation:</span><span class="sxs-lookup"><span data-stu-id="b066e-422">In addition to running periodically on a schedule, an indexer can also be invoked on demand via the **Run Indexer** operation:</span></span> 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-423">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-423">The `api-version` is required.</span></span> <span data-ttu-id="b066e-424">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-424">The preview version is `2015-02-28-Preview`.</span></span> 

<span data-ttu-id="b066e-425">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-425">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-426">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-426">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-427">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-427">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-428">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-428">**Response**</span></span>

<span data-ttu-id="b066e-429">Status Code: 202 Accepted is returned for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-429">Status Code: 202 Accepted is returned for a successful response.</span></span>

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a><span data-ttu-id="b066e-430">Get Indexer Status</span><span class="sxs-lookup"><span data-stu-id="b066e-430">Get Indexer Status</span></span>
<span data-ttu-id="b066e-431">The **Get Indexer Status** operation retrieves the current status and execution history of an indexer:</span><span class="sxs-lookup"><span data-stu-id="b066e-431">The **Get Indexer Status** operation retrieves the current status and execution history of an indexer:</span></span> 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


<span data-ttu-id="b066e-432">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-432">The `api-version` is required.</span></span> <span data-ttu-id="b066e-433">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-433">The preview version is `2015-02-28-Preview`.</span></span> 

<span data-ttu-id="b066e-434">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-434">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-435">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-435">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-436">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-436">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-437">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-437">**Response**</span></span>

<span data-ttu-id="b066e-438">Status Code: 200 OK for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-438">Status Code: 200 OK for a successful response.</span></span>

<span data-ttu-id="b066e-439">The response body contains information about overall indexer health status, the last indexer invocation, as well as the history of recent indexer invocations (if present).</span><span class="sxs-lookup"><span data-stu-id="b066e-439">The response body contains information about overall indexer health status, the last indexer invocation, as well as the history of recent indexer invocations (if present).</span></span> 

<span data-ttu-id="b066e-440">A sample response body looks like this:</span><span class="sxs-lookup"><span data-stu-id="b066e-440">A sample response body looks like this:</span></span> 

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

<span data-ttu-id="b066e-441">**Indexer Status**</span><span class="sxs-lookup"><span data-stu-id="b066e-441">**Indexer Status**</span></span>

<span data-ttu-id="b066e-442">Indexer status can be one of the following  values:</span><span class="sxs-lookup"><span data-stu-id="b066e-442">Indexer status can be one of the following  values:</span></span>

* <span data-ttu-id="b066e-443">`running` indicates that the indexer is running normally.</span><span class="sxs-lookup"><span data-stu-id="b066e-443">`running` indicates that the indexer is running normally.</span></span> <span data-ttu-id="b066e-444">Note that some of the indexer executions may still be failing, so it's a good idea to check the `lastResult` property as well.</span><span class="sxs-lookup"><span data-stu-id="b066e-444">Note that some of the indexer executions may still be failing, so it's a good idea to check the `lastResult` property as well.</span></span> 
* <span data-ttu-id="b066e-445">`error` indicates that the indexer experienced an error that cannot be corrected without human intervention.</span><span class="sxs-lookup"><span data-stu-id="b066e-445">`error` indicates that the indexer experienced an error that cannot be corrected without human intervention.</span></span> <span data-ttu-id="b066e-446">For example, the data source credentials may have expired, or the schema of the data source or of the target index has changed in a breaking way.</span><span class="sxs-lookup"><span data-stu-id="b066e-446">For example, the data source credentials may have expired, or the schema of the data source or of the target index has changed in a breaking way.</span></span> 

<span data-ttu-id="b066e-447">**Indexer Execution Result**</span><span class="sxs-lookup"><span data-stu-id="b066e-447">**Indexer Execution Result**</span></span>

<span data-ttu-id="b066e-448">An indexer execution result contains information about a single indexer execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-448">An indexer execution result contains information about a single indexer execution.</span></span> <span data-ttu-id="b066e-449">The latest result is surfaced as the `lastResult` property of the indexer status.</span><span class="sxs-lookup"><span data-stu-id="b066e-449">The latest result is surfaced as the `lastResult` property of the indexer status.</span></span> <span data-ttu-id="b066e-450">Other recent results, if present, are returned as the `executionHistory` property of the indexer status.</span><span class="sxs-lookup"><span data-stu-id="b066e-450">Other recent results, if present, are returned as the `executionHistory` property of the indexer status.</span></span> 

<span data-ttu-id="b066e-451">Indexer execution result contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="b066e-451">Indexer execution result contains the following properties:</span></span> 

* <span data-ttu-id="b066e-452">`status`: the status of an execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-452">`status`: the status of an execution.</span></span> <span data-ttu-id="b066e-453">See [Indexer Execution Status](#IndexerExecutionStatus) below for details.</span><span class="sxs-lookup"><span data-stu-id="b066e-453">See [Indexer Execution Status](#IndexerExecutionStatus) below for details.</span></span> 
* <span data-ttu-id="b066e-454">`errorMessage`: error message for a failed execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-454">`errorMessage`: error message for a failed execution.</span></span> 
* <span data-ttu-id="b066e-455">`startTime`: the time in UTC when this execution started.</span><span class="sxs-lookup"><span data-stu-id="b066e-455">`startTime`: the time in UTC when this execution started.</span></span>
* <span data-ttu-id="b066e-456">`endTime`: the time in UTC when this execution ended.</span><span class="sxs-lookup"><span data-stu-id="b066e-456">`endTime`: the time in UTC when this execution ended.</span></span> <span data-ttu-id="b066e-457">This value is not set if the execution is still in progress.</span><span class="sxs-lookup"><span data-stu-id="b066e-457">This value is not set if the execution is still in progress.</span></span>
* <span data-ttu-id="b066e-458">`errors`: an array of item-level errors, if any.</span><span class="sxs-lookup"><span data-stu-id="b066e-458">`errors`: an array of item-level errors, if any.</span></span> <span data-ttu-id="b066e-459">Each entry contains a document key (`key` property) and an error message (`errorMessage` property).</span><span class="sxs-lookup"><span data-stu-id="b066e-459">Each entry contains a document key (`key` property) and an error message (`errorMessage` property).</span></span> 
* <span data-ttu-id="b066e-460">`itemsProcessed`: the number of data source items (for example, table rows) that the indexer attempted to index during this execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-460">`itemsProcessed`: the number of data source items (for example, table rows) that the indexer attempted to index during this execution.</span></span> 
* <span data-ttu-id="b066e-461">`itemsFailed`: the number of items that failed during this execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-461">`itemsFailed`: the number of items that failed during this execution.</span></span>  
* <span data-ttu-id="b066e-462">`initialTrackingState`: always `null` for the first indexer execution, or if the data change tracking policy is not enabled on the data source used.</span><span class="sxs-lookup"><span data-stu-id="b066e-462">`initialTrackingState`: always `null` for the first indexer execution, or if the data change tracking policy is not enabled on the data source used.</span></span> <span data-ttu-id="b066e-463">If such a policy is enabled, in subsequent executions this value indicates the first (lowest) change tracking value processed by this execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-463">If such a policy is enabled, in subsequent executions this value indicates the first (lowest) change tracking value processed by this execution.</span></span> 
* <span data-ttu-id="b066e-464">`finalTrackingState`: always `null` if the data change tracking policy is not enabled on the data source used.</span><span class="sxs-lookup"><span data-stu-id="b066e-464">`finalTrackingState`: always `null` if the data change tracking policy is not enabled on the data source used.</span></span> <span data-ttu-id="b066e-465">Otherwise, indicates the latest (highest) change tracking value successfully processed by this execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-465">Otherwise, indicates the latest (highest) change tracking value successfully processed by this execution.</span></span> 

<a name="IndexerExecutionStatus"></a>
<span data-ttu-id="b066e-466">**Indexer Execution Status**</span><span class="sxs-lookup"><span data-stu-id="b066e-466">**Indexer Execution Status**</span></span>

<span data-ttu-id="b066e-467">Indexer execution status captures the status of a single indexer execution.</span><span class="sxs-lookup"><span data-stu-id="b066e-467">Indexer execution status captures the status of a single indexer execution.</span></span> <span data-ttu-id="b066e-468">It can have the following values:</span><span class="sxs-lookup"><span data-stu-id="b066e-468">It can have the following values:</span></span>

* <span data-ttu-id="b066e-469">`success` indicates that the indexer execution has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="b066e-469">`success` indicates that the indexer execution has completed successfully.</span></span>
* <span data-ttu-id="b066e-470">`inProgress` indicates that the indexer execution is in progress.</span><span class="sxs-lookup"><span data-stu-id="b066e-470">`inProgress` indicates that the indexer execution is in progress.</span></span> 
* <span data-ttu-id="b066e-471">`transientFailure` indicates that an indexer execution has failed.</span><span class="sxs-lookup"><span data-stu-id="b066e-471">`transientFailure` indicates that an indexer execution has failed.</span></span> <span data-ttu-id="b066e-472">See `errorMessage` property for details.</span><span class="sxs-lookup"><span data-stu-id="b066e-472">See `errorMessage` property for details.</span></span> <span data-ttu-id="b066e-473">The failure may or may not require human intervention to fix - for example, fixing a schema incompatibility between the data source and the target index requires user action, while a temporary data source downtime does not.</span><span class="sxs-lookup"><span data-stu-id="b066e-473">The failure may or may not require human intervention to fix - for example, fixing a schema incompatibility between the data source and the target index requires user action, while a temporary data source downtime does not.</span></span> <span data-ttu-id="b066e-474">Indexer invocations will continue per schedule, if one is present.</span><span class="sxs-lookup"><span data-stu-id="b066e-474">Indexer invocations will continue per schedule, if one is present.</span></span> 
* <span data-ttu-id="b066e-475">`persistentFailure` indicates that the indexer has failed in a way that requires human intervention.</span><span class="sxs-lookup"><span data-stu-id="b066e-475">`persistentFailure` indicates that the indexer has failed in a way that requires human intervention.</span></span> <span data-ttu-id="b066e-476">Scheduled indexer executions stop.</span><span class="sxs-lookup"><span data-stu-id="b066e-476">Scheduled indexer executions stop.</span></span> <span data-ttu-id="b066e-477">After addressing the issue, use Reset Indexer API to restart the scheduled executions.</span><span class="sxs-lookup"><span data-stu-id="b066e-477">After addressing the issue, use Reset Indexer API to restart the scheduled executions.</span></span> 
* <span data-ttu-id="b066e-478">`reset` indicates that the indexer has been reset by a call to Reset Indexer API (see below).</span><span class="sxs-lookup"><span data-stu-id="b066e-478">`reset` indicates that the indexer has been reset by a call to Reset Indexer API (see below).</span></span> 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a><span data-ttu-id="b066e-479">Reset Indexer</span><span class="sxs-lookup"><span data-stu-id="b066e-479">Reset Indexer</span></span>
<span data-ttu-id="b066e-480">The **Reset Indexer** operation resets the change tracking state associated with the indexer.</span><span class="sxs-lookup"><span data-stu-id="b066e-480">The **Reset Indexer** operation resets the change tracking state associated with the indexer.</span></span> <span data-ttu-id="b066e-481">This allows you to trigger from-scratch re-indexing (for example, if your data source schema has changed), or to change the data change detection policy for a data source associated with the indexer.</span><span class="sxs-lookup"><span data-stu-id="b066e-481">This allows you to trigger from-scratch re-indexing (for example, if your data source schema has changed), or to change the data change detection policy for a data source associated with the indexer.</span></span>   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="b066e-482">The `api-version` is required.</span><span class="sxs-lookup"><span data-stu-id="b066e-482">The `api-version` is required.</span></span> <span data-ttu-id="b066e-483">The preview version is `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="b066e-483">The preview version is `2015-02-28-Preview`.</span></span> 

<span data-ttu-id="b066e-484">The `api-key` must be an admin key (as opposed to a query key).</span><span class="sxs-lookup"><span data-stu-id="b066e-484">The `api-key` must be an admin key (as opposed to a query key).</span></span> <span data-ttu-id="b066e-485">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span><span class="sxs-lookup"><span data-stu-id="b066e-485">Refer to the authentication section in [Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) to learn more about keys.</span></span> <span data-ttu-id="b066e-486">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span><span class="sxs-lookup"><span data-stu-id="b066e-486">[Create a Search service in the portal](search-create-service-portal.md) explains how to get the service URL and key properties used in the request.</span></span>

<span data-ttu-id="b066e-487">**Response**</span><span class="sxs-lookup"><span data-stu-id="b066e-487">**Response**</span></span>

<span data-ttu-id="b066e-488">Status Code: 204 No Content for a successful response.</span><span class="sxs-lookup"><span data-stu-id="b066e-488">Status Code: 204 No Content for a successful response.</span></span>

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a><span data-ttu-id="b066e-489">Mapping between SQL Data Types and Azure Search Data Types</span><span class="sxs-lookup"><span data-stu-id="b066e-489">Mapping between SQL Data Types and Azure Search Data Types</span></span>
<table style="font-size:12">
<tr>
<td><span data-ttu-id="b066e-490">SQL data type</span><span class="sxs-lookup"><span data-stu-id="b066e-490">SQL data type</span></span></td>    
<td><span data-ttu-id="b066e-491">Allowed target index field types</span><span class="sxs-lookup"><span data-stu-id="b066e-491">Allowed target index field types</span></span></td>
<td><span data-ttu-id="b066e-492">Notes</span><span class="sxs-lookup"><span data-stu-id="b066e-492">Notes</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-493">bit</span><span class="sxs-lookup"><span data-stu-id="b066e-493">bit</span></span></td>
<td><span data-ttu-id="b066e-494">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-494">Edm.Boolean, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-495">int, smallint, tinyint</span><span class="sxs-lookup"><span data-stu-id="b066e-495">int, smallint, tinyint</span></span></td>
<td><span data-ttu-id="b066e-496">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-496">Edm.Int32, Edm.Int64, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-497">bigint</span><span class="sxs-lookup"><span data-stu-id="b066e-497">bigint</span></span></td>
<td><span data-ttu-id="b066e-498">Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-498">Edm.Int64, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-499">real, float</span><span class="sxs-lookup"><span data-stu-id="b066e-499">real, float</span></span></td>
<td><span data-ttu-id="b066e-500">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-500">Edm.Double, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-501">smallmoney, money</span><span class="sxs-lookup"><span data-stu-id="b066e-501">smallmoney, money</span></span><br><span data-ttu-id="b066e-502">decimal</span><span class="sxs-lookup"><span data-stu-id="b066e-502">decimal</span></span><br><span data-ttu-id="b066e-503">numeric</span><span class="sxs-lookup"><span data-stu-id="b066e-503">numeric</span></span>
</td>
<td><span data-ttu-id="b066e-504">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-504">Edm.String</span></span></td>
<td><span data-ttu-id="b066e-505">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span><span class="sxs-lookup"><span data-stu-id="b066e-505">Azure Search does not support converting decimal types into Edm.Double because this would lose precision</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="b066e-506">char, nchar, varchar, nvarchar</span><span class="sxs-lookup"><span data-stu-id="b066e-506">char, nchar, varchar, nvarchar</span></span></td>
<td><span data-ttu-id="b066e-507">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-507">Edm.String</span></span><br/><span data-ttu-id="b066e-508">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="b066e-508">Collection(Edm.String)</span></span></td>
<td><span data-ttu-id="b066e-509">See [Field Mapping Functions](#FieldMappingFunctions) in this document for details on how to transform a string column into a Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="b066e-509">See [Field Mapping Functions](#FieldMappingFunctions) in this document for details on how to transform a string column into a Collection(Edm.String)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-510">smalldatetime, datetime, datetime2, date, datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b066e-510">smalldatetime, datetime, datetime2, date, datetimeoffset</span></span></td>
<td><span data-ttu-id="b066e-511">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-511">Edm.DateTimeOffset, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-512">uniqueidentifer</span><span class="sxs-lookup"><span data-stu-id="b066e-512">uniqueidentifer</span></span></td>
<td><span data-ttu-id="b066e-513">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-513">Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-514">geography</span><span class="sxs-lookup"><span data-stu-id="b066e-514">geography</span></span></td>
<td><span data-ttu-id="b066e-515">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="b066e-515">Edm.GeographyPoint</span></span></td>
<td><span data-ttu-id="b066e-516">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span><span class="sxs-lookup"><span data-stu-id="b066e-516">Only geography instances of type POINT with SRID 4326 (which is the default) are supported</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-517">rowversion</span><span class="sxs-lookup"><span data-stu-id="b066e-517">rowversion</span></span></td>
<td><span data-ttu-id="b066e-518">N/A</span><span class="sxs-lookup"><span data-stu-id="b066e-518">N/A</span></span></td>
<td><span data-ttu-id="b066e-519">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span><span class="sxs-lookup"><span data-stu-id="b066e-519">Row-version columns cannot be stored in the search index, but they can be used for change tracking</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-520">time, timespan</span><span class="sxs-lookup"><span data-stu-id="b066e-520">time, timespan</span></span><br><span data-ttu-id="b066e-521">binary, varbinary, image,</span><span class="sxs-lookup"><span data-stu-id="b066e-521">binary, varbinary, image,</span></span><br><span data-ttu-id="b066e-522">xml, geometry, CLR types</span><span class="sxs-lookup"><span data-stu-id="b066e-522">xml, geometry, CLR types</span></span></td>
<td><span data-ttu-id="b066e-523">N/A</span><span class="sxs-lookup"><span data-stu-id="b066e-523">N/A</span></span></td>
<td><span data-ttu-id="b066e-524">Not supported</span><span class="sxs-lookup"><span data-stu-id="b066e-524">Not supported</span></span></td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a><span data-ttu-id="b066e-525">Mapping between JSON Data Types and Azure Search Data Types</span><span class="sxs-lookup"><span data-stu-id="b066e-525">Mapping between JSON Data Types and Azure Search Data Types</span></span>
<table style="font-size:12">
<tr>
<td><span data-ttu-id="b066e-526">JSON data type</span><span class="sxs-lookup"><span data-stu-id="b066e-526">JSON data type</span></span></td>    
<td><span data-ttu-id="b066e-527">Allowed target index field types</span><span class="sxs-lookup"><span data-stu-id="b066e-527">Allowed target index field types</span></span></td>
<td><span data-ttu-id="b066e-528">Notes</span><span class="sxs-lookup"><span data-stu-id="b066e-528">Notes</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-529">bool</span><span class="sxs-lookup"><span data-stu-id="b066e-529">bool</span></span></td>
<td><span data-ttu-id="b066e-530">Edm.Boolean, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-530">Edm.Boolean, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-531">Integral numbers</span><span class="sxs-lookup"><span data-stu-id="b066e-531">Integral numbers</span></span></td>
<td><span data-ttu-id="b066e-532">Edm.Int32, Edm.Int64, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-532">Edm.Int32, Edm.Int64, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-533">Floating-point numbers</span><span class="sxs-lookup"><span data-stu-id="b066e-533">Floating-point numbers</span></span></td>
<td><span data-ttu-id="b066e-534">Edm.Double, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-534">Edm.Double, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-535">string</span><span class="sxs-lookup"><span data-stu-id="b066e-535">string</span></span></td>
<td><span data-ttu-id="b066e-536">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-536">Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-537">arrays of primitive types, e.g. [ "a", "b", "c" ]</span><span class="sxs-lookup"><span data-stu-id="b066e-537">arrays of primitive types, e.g. [ "a", "b", "c" ]</span></span></td>
<td><span data-ttu-id="b066e-538">Collection(Edm.String)</span><span class="sxs-lookup"><span data-stu-id="b066e-538">Collection(Edm.String)</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-539">Strings that look like dates</span><span class="sxs-lookup"><span data-stu-id="b066e-539">Strings that look like dates</span></span></td>
<td><span data-ttu-id="b066e-540">Edm.DateTimeOffset, Edm.String</span><span class="sxs-lookup"><span data-stu-id="b066e-540">Edm.DateTimeOffset, Edm.String</span></span></td>
<td></td>
</tr>
<tr>
<td><span data-ttu-id="b066e-541">GeoJSON point objects</span><span class="sxs-lookup"><span data-stu-id="b066e-541">GeoJSON point objects</span></span></td>
<td><span data-ttu-id="b066e-542">Edm.GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="b066e-542">Edm.GeographyPoint</span></span></td>
<td><span data-ttu-id="b066e-543">GeoJSON points are JSON objects in the following format: { "type" : "Point", "coordinates" : [long, lat] }</span><span class="sxs-lookup"><span data-stu-id="b066e-543">GeoJSON points are JSON objects in the following format: { "type" : "Point", "coordinates" : [long, lat] }</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="b066e-544">Other JSON objects</span><span class="sxs-lookup"><span data-stu-id="b066e-544">Other JSON objects</span></span></td>
<td><span data-ttu-id="b066e-545">N/A</span><span class="sxs-lookup"><span data-stu-id="b066e-545">N/A</span></span></td>
<td><span data-ttu-id="b066e-546">Not supported; Azure Search currently supports only primitive types and string collections</span><span class="sxs-lookup"><span data-stu-id="b066e-546">Not supported; Azure Search currently supports only primitive types and string collections</span></span></td>
</tr>
</table>
