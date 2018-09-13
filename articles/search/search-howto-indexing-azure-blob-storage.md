---
title: Indexing Azure Blob Storage with Azure Search
description: Learn how to index Azure Blob Storage and extract text from documents with Azure Search
services: search
documentationcenter: ''
author: chaosrealm
manager: pablocas
editor: ''
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/15/2017
ms.author: eugenesh
ms.openlocfilehash: c74c8fb892103a00b0bdfcfeaa2ecd6c3188251e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551175"
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a><span data-ttu-id="08da2-103">Indexing Documents in Azure Blob Storage with Azure Search</span><span class="sxs-lookup"><span data-stu-id="08da2-103">Indexing Documents in Azure Blob Storage with Azure Search</span></span>
<span data-ttu-id="08da2-104">This article shows how to use Azure Search to index documents (such as PDFs, Microsoft Office documents, and several other common formats) stored in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="08da2-104">This article shows how to use Azure Search to index documents (such as PDFs, Microsoft Office documents, and several other common formats) stored in Azure Blob storage.</span></span> <span data-ttu-id="08da2-105">First, it explains the basics of setting up and configuring a blob indexer.</span><span class="sxs-lookup"><span data-stu-id="08da2-105">First, it explains the basics of setting up and configuring a blob indexer.</span></span> <span data-ttu-id="08da2-106">Then, it offers a deeper exploration of behaviors and scenarios you are likely to encounter.</span><span class="sxs-lookup"><span data-stu-id="08da2-106">Then, it offers a deeper exploration of behaviors and scenarios you are likely to encounter.</span></span>

## <a name="supported-document-formats"></a><span data-ttu-id="08da2-107">Supported document formats</span><span class="sxs-lookup"><span data-stu-id="08da2-107">Supported document formats</span></span>
<span data-ttu-id="08da2-108">The blob indexer can extract text from the following document formats:</span><span class="sxs-lookup"><span data-stu-id="08da2-108">The blob indexer can extract text from the following document formats:</span></span>

* <span data-ttu-id="08da2-109">PDF</span><span class="sxs-lookup"><span data-stu-id="08da2-109">PDF</span></span>
* <span data-ttu-id="08da2-110">Microsoft Office formats: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook emails)</span><span class="sxs-lookup"><span data-stu-id="08da2-110">Microsoft Office formats: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook emails)</span></span>  
* <span data-ttu-id="08da2-111">HTML</span><span class="sxs-lookup"><span data-stu-id="08da2-111">HTML</span></span>
* <span data-ttu-id="08da2-112">XML</span><span class="sxs-lookup"><span data-stu-id="08da2-112">XML</span></span>
* <span data-ttu-id="08da2-113">ZIP</span><span class="sxs-lookup"><span data-stu-id="08da2-113">ZIP</span></span>
* <span data-ttu-id="08da2-114">EML</span><span class="sxs-lookup"><span data-stu-id="08da2-114">EML</span></span>
* <span data-ttu-id="08da2-115">Plain text files</span><span class="sxs-lookup"><span data-stu-id="08da2-115">Plain text files</span></span>  
* <span data-ttu-id="08da2-116">JSON (see [Indexing JSON blobs](search-howto-index-json-blobs.md) preview feature)</span><span class="sxs-lookup"><span data-stu-id="08da2-116">JSON (see [Indexing JSON blobs](search-howto-index-json-blobs.md) preview feature)</span></span>
* <span data-ttu-id="08da2-117">CSV (see [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview feature)</span><span class="sxs-lookup"><span data-stu-id="08da2-117">CSV (see [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview feature)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08da2-118">Support for CSV and JSON arrays is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="08da2-118">Support for CSV and JSON arrays is currently in preview.</span></span> <span data-ttu-id="08da2-119">These formats are available only using version **2015-02-28-Preview** of the REST API or version 2.x-preview of the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="08da2-119">These formats are available only using version **2015-02-28-Preview** of the REST API or version 2.x-preview of the .NET SDK.</span></span> <span data-ttu-id="08da2-120">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="08da2-120">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
>
>

## <a name="setting-up-blob-indexing"></a><span data-ttu-id="08da2-121">Setting up blob indexing</span><span class="sxs-lookup"><span data-stu-id="08da2-121">Setting up blob indexing</span></span>
<span data-ttu-id="08da2-122">You can set up an Azure Blob Storage indexer using:</span><span class="sxs-lookup"><span data-stu-id="08da2-122">You can set up an Azure Blob Storage indexer using:</span></span>

* [<span data-ttu-id="08da2-123">Azure portal</span><span class="sxs-lookup"><span data-stu-id="08da2-123">Azure portal</span></span>](https://ms.portal.azure.com)
* <span data-ttu-id="08da2-124">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span><span class="sxs-lookup"><span data-stu-id="08da2-124">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span></span>
* <span data-ttu-id="08da2-125">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span><span class="sxs-lookup"><span data-stu-id="08da2-125">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-126">Some features (for example, field mappings) are not yet available in the portal, and have to be used programmatically.</span><span class="sxs-lookup"><span data-stu-id="08da2-126">Some features (for example, field mappings) are not yet available in the portal, and have to be used programmatically.</span></span>
>
>

<span data-ttu-id="08da2-127">Here, we demonstrate the flow using the REST API.</span><span class="sxs-lookup"><span data-stu-id="08da2-127">Here, we demonstrate the flow using the REST API.</span></span>

### <a name="step-1-create-a-data-source"></a><span data-ttu-id="08da2-128">Step 1: Create a data source</span><span class="sxs-lookup"><span data-stu-id="08da2-128">Step 1: Create a data source</span></span>
<span data-ttu-id="08da2-129">A data source specifies which data to index, credentials needed to access the data, and policies to efficiently identify changes in the data (new, modified, or deleted rows).</span><span class="sxs-lookup"><span data-stu-id="08da2-129">A data source specifies which data to index, credentials needed to access the data, and policies to efficiently identify changes in the data (new, modified, or deleted rows).</span></span> <span data-ttu-id="08da2-130">A data source can be used by multiple indexers in the same search service.</span><span class="sxs-lookup"><span data-stu-id="08da2-130">A data source can be used by multiple indexers in the same search service.</span></span>

<span data-ttu-id="08da2-131">For blob indexing, the data source must have the following required properties:</span><span class="sxs-lookup"><span data-stu-id="08da2-131">For blob indexing, the data source must have the following required properties:</span></span>

* <span data-ttu-id="08da2-132">**name** is the unique name of the data source within your search service.</span><span class="sxs-lookup"><span data-stu-id="08da2-132">**name** is the unique name of the data source within your search service.</span></span>
* <span data-ttu-id="08da2-133">**type** must be `azureblob`.</span><span class="sxs-lookup"><span data-stu-id="08da2-133">**type** must be `azureblob`.</span></span>
* <span data-ttu-id="08da2-134">**credentials** provides the storage account connection string as the `credentials.connectionString` parameter.</span><span class="sxs-lookup"><span data-stu-id="08da2-134">**credentials** provides the storage account connection string as the `credentials.connectionString` parameter.</span></span> <span data-ttu-id="08da2-135">See [How to specify credentials](#Credentials) below for details.</span><span class="sxs-lookup"><span data-stu-id="08da2-135">See [How to specify credentials](#Credentials) below for details.</span></span>
* <span data-ttu-id="08da2-136">**container** specifies a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="08da2-136">**container** specifies a container in your storage account.</span></span> <span data-ttu-id="08da2-137">By default, all blobs within the container are retrievable.</span><span class="sxs-lookup"><span data-stu-id="08da2-137">By default, all blobs within the container are retrievable.</span></span> <span data-ttu-id="08da2-138">If you only want to index blobs in a particular virtual directory, you can specify that directory using the optional **query** parameter.</span><span class="sxs-lookup"><span data-stu-id="08da2-138">If you only want to index blobs in a particular virtual directory, you can specify that directory using the optional **query** parameter.</span></span>

<span data-ttu-id="08da2-139">To create a data source:</span><span class="sxs-lookup"><span data-stu-id="08da2-139">To create a data source:</span></span>

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

<span data-ttu-id="08da2-140">For more on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span><span class="sxs-lookup"><span data-stu-id="08da2-140">For more on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span></span>

<a name="Credentials"></a>
#### <a name="how-to-specify-credentials"></a><span data-ttu-id="08da2-141">How to specify credentials</span><span class="sxs-lookup"><span data-stu-id="08da2-141">How to specify credentials</span></span> ####

<span data-ttu-id="08da2-142">You can provide the credentials for the blob container in one of these ways:</span><span class="sxs-lookup"><span data-stu-id="08da2-142">You can provide the credentials for the blob container in one of these ways:</span></span>

- <span data-ttu-id="08da2-143">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`.</span><span class="sxs-lookup"><span data-stu-id="08da2-143">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`.</span></span> <span data-ttu-id="08da2-144">You can get the connection string from the Azure portal by navigating to the storage account blade > Settings > Keys (for Classic storage accounts) or Settings > Access keys (for Azure Resource Manager storage accounts).</span><span class="sxs-lookup"><span data-stu-id="08da2-144">You can get the connection string from the Azure portal by navigating to the storage account blade > Settings > Keys (for Classic storage accounts) or Settings > Access keys (for Azure Resource Manager storage accounts).</span></span>
- <span data-ttu-id="08da2-145">**Storage account shared access signature** (SAS) connection string: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=b&sp=rl`.</span><span class="sxs-lookup"><span data-stu-id="08da2-145">**Storage account shared access signature** (SAS) connection string: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=b&sp=rl`.</span></span> <span data-ttu-id="08da2-146">The SAS should have the list and read permissions on containers and objects (blobs in this case).</span><span class="sxs-lookup"><span data-stu-id="08da2-146">The SAS should have the list and read permissions on containers and objects (blobs in this case).</span></span>
-  <span data-ttu-id="08da2-147">**Container shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<the signature>&se=<the validity end time>&sp=rl`.</span><span class="sxs-lookup"><span data-stu-id="08da2-147">**Container shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<the signature>&se=<the validity end time>&sp=rl`.</span></span> <span data-ttu-id="08da2-148">The SAS should have the list and read permissions on the container.</span><span class="sxs-lookup"><span data-stu-id="08da2-148">The SAS should have the list and read permissions on the container.</span></span>

<span data-ttu-id="08da2-149">For more info on storage shared access signatures, see [Using Shared Access Signatures](../storage/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="08da2-149">For more info on storage shared access signatures, see [Using Shared Access Signatures](../storage/storage-dotnet-shared-access-signature-part-1.md).</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-150">If you use SAS credentials, you will need to update the data source credentials periodically with renewed signatures to prevent their expiration.</span><span class="sxs-lookup"><span data-stu-id="08da2-150">If you use SAS credentials, you will need to update the data source credentials periodically with renewed signatures to prevent their expiration.</span></span> <span data-ttu-id="08da2-151">If SAS credentials expire, the indexer will fail with an error message similar to `Credentials provided in the connection string are invalid or have expired.`.</span><span class="sxs-lookup"><span data-stu-id="08da2-151">If SAS credentials expire, the indexer will fail with an error message similar to `Credentials provided in the connection string are invalid or have expired.`.</span></span>  

### <a name="step-2-create-an-index"></a><span data-ttu-id="08da2-152">Step 2: Create an index</span><span class="sxs-lookup"><span data-stu-id="08da2-152">Step 2: Create an index</span></span>
<span data-ttu-id="08da2-153">The index specifies the fields in a document, attributes, and other constructs that shape the search experience.</span><span class="sxs-lookup"><span data-stu-id="08da2-153">The index specifies the fields in a document, attributes, and other constructs that shape the search experience.</span></span>

<span data-ttu-id="08da2-154">Here's how to create an index with a searchable `content` field to store the text extracted from blobs:</span><span class="sxs-lookup"><span data-stu-id="08da2-154">Here's how to create an index with a searchable `content` field to store the text extracted from blobs:</span></span>   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

<span data-ttu-id="08da2-155">For more on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)</span><span class="sxs-lookup"><span data-stu-id="08da2-155">For more on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)</span></span>

### <a name="step-3-create-an-indexer"></a><span data-ttu-id="08da2-156">Step 3: Create an indexer</span><span class="sxs-lookup"><span data-stu-id="08da2-156">Step 3: Create an indexer</span></span>
<span data-ttu-id="08da2-157">An indexer connects a data source with a target search index, and provides a schedule to automate the data refresh.</span><span class="sxs-lookup"><span data-stu-id="08da2-157">An indexer connects a data source with a target search index, and provides a schedule to automate the data refresh.</span></span>

<span data-ttu-id="08da2-158">Once the index and data source have been created, you're ready to create the indexer:</span><span class="sxs-lookup"><span data-stu-id="08da2-158">Once the index and data source have been created, you're ready to create the indexer:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

<span data-ttu-id="08da2-159">This indexer will run every two hours (schedule interval is set to "PT2H").</span><span class="sxs-lookup"><span data-stu-id="08da2-159">This indexer will run every two hours (schedule interval is set to "PT2H").</span></span> <span data-ttu-id="08da2-160">To run an indexer every 30 minutes, set the interval to "PT30M".</span><span class="sxs-lookup"><span data-stu-id="08da2-160">To run an indexer every 30 minutes, set the interval to "PT30M".</span></span> <span data-ttu-id="08da2-161">The shortest supported interval is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="08da2-161">The shortest supported interval is 5 minutes.</span></span> <span data-ttu-id="08da2-162">The schedule is optional - if omitted, an indexer runs only once when it's created.</span><span class="sxs-lookup"><span data-stu-id="08da2-162">The schedule is optional - if omitted, an indexer runs only once when it's created.</span></span> <span data-ttu-id="08da2-163">However, you can run an indexer on-demand at any time.</span><span class="sxs-lookup"><span data-stu-id="08da2-163">However, you can run an indexer on-demand at any time.</span></span>   

<span data-ttu-id="08da2-164">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span><span class="sxs-lookup"><span data-stu-id="08da2-164">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span></span>

## <a name="how-azure-search-indexes-blobs"></a><span data-ttu-id="08da2-165">How Azure Search indexes blobs</span><span class="sxs-lookup"><span data-stu-id="08da2-165">How Azure Search indexes blobs</span></span>

<span data-ttu-id="08da2-166">Depending on the [indexer configuration](#PartsOfBlobToIndex), the blob indexer can index storage metadata only (useful when you only care about the metadata and don't need to index the content of blobs), storage and content metadata, or both metadata and textual content.</span><span class="sxs-lookup"><span data-stu-id="08da2-166">Depending on the [indexer configuration](#PartsOfBlobToIndex), the blob indexer can index storage metadata only (useful when you only care about the metadata and don't need to index the content of blobs), storage and content metadata, or both metadata and textual content.</span></span> <span data-ttu-id="08da2-167">By default, the indexer extracts both metadata and content.</span><span class="sxs-lookup"><span data-stu-id="08da2-167">By default, the indexer extracts both metadata and content.</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-168">By default, blobs with structured content such as JSON or CSV are indexed as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="08da2-168">By default, blobs with structured content such as JSON or CSV are indexed as a single chunk of text.</span></span> <span data-ttu-id="08da2-169">If you want to index JSON and CSV blobs in a structured way, see [Indexing JSON blobs](search-howto-index-json-blobs.md) and [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview features.</span><span class="sxs-lookup"><span data-stu-id="08da2-169">If you want to index JSON and CSV blobs in a structured way, see [Indexing JSON blobs](search-howto-index-json-blobs.md) and [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview features.</span></span>
> 
> <span data-ttu-id="08da2-170">A compound or embedded document (such as a ZIP archive or a Word document with embedded Outlook email containing attachments) is also indexed as a single document.</span><span class="sxs-lookup"><span data-stu-id="08da2-170">A compound or embedded document (such as a ZIP archive or a Word document with embedded Outlook email containing attachments) is also indexed as a single document.</span></span>

* <span data-ttu-id="08da2-171">The textual content of the document is extracted into a string field named `content`.</span><span class="sxs-lookup"><span data-stu-id="08da2-171">The textual content of the document is extracted into a string field named `content`.</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-172">Azure Search limits how much text it extracts depending on the pricing tier: 32,000 characters for Free tier, 64,000 for Basic, and 4 million for Standard, Standard S2 and Standard S3 tiers.</span><span class="sxs-lookup"><span data-stu-id="08da2-172">Azure Search limits how much text it extracts depending on the pricing tier: 32,000 characters for Free tier, 64,000 for Basic, and 4 million for Standard, Standard S2 and Standard S3 tiers.</span></span> <span data-ttu-id="08da2-173">A warning is included in the indexer status response for truncated documents.</span><span class="sxs-lookup"><span data-stu-id="08da2-173">A warning is included in the indexer status response for truncated documents.</span></span>  

* <span data-ttu-id="08da2-174">User-specified metadata properties present on the blob, if any, are extracted verbatim.</span><span class="sxs-lookup"><span data-stu-id="08da2-174">User-specified metadata properties present on the blob, if any, are extracted verbatim.</span></span>
* <span data-ttu-id="08da2-175">Standard blob metadata properties are extracted into the following fields:</span><span class="sxs-lookup"><span data-stu-id="08da2-175">Standard blob metadata properties are extracted into the following fields:</span></span>

  * <span data-ttu-id="08da2-176">**metadata\_storage\_name** (Edm.String) - the file name of the blob.</span><span class="sxs-lookup"><span data-stu-id="08da2-176">**metadata\_storage\_name** (Edm.String) - the file name of the blob.</span></span> <span data-ttu-id="08da2-177">For example, if you have a blob /my-container/my-folder/subfolder/resume.pdf, the value of this field is `resume.pdf`.</span><span class="sxs-lookup"><span data-stu-id="08da2-177">For example, if you have a blob /my-container/my-folder/subfolder/resume.pdf, the value of this field is `resume.pdf`.</span></span>
  * <span data-ttu-id="08da2-178">**metadata\_storage\_path** (Edm.String) - the full URI of the blob, including the storage account.</span><span class="sxs-lookup"><span data-stu-id="08da2-178">**metadata\_storage\_path** (Edm.String) - the full URI of the blob, including the storage account.</span></span> <span data-ttu-id="08da2-179">For example, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`</span><span class="sxs-lookup"><span data-stu-id="08da2-179">For example, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`</span></span>
  * <span data-ttu-id="08da2-180">**metadata\_storage\_content\_type** (Edm.String) - content type as specified by the code you used to upload the blob.</span><span class="sxs-lookup"><span data-stu-id="08da2-180">**metadata\_storage\_content\_type** (Edm.String) - content type as specified by the code you used to upload the blob.</span></span> <span data-ttu-id="08da2-181">For example, `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="08da2-181">For example, `application/octet-stream`.</span></span>
  * <span data-ttu-id="08da2-182">**metadata\_storage\_last\_modified** (Edm.DateTimeOffset) - last modified timestamp for the blob.</span><span class="sxs-lookup"><span data-stu-id="08da2-182">**metadata\_storage\_last\_modified** (Edm.DateTimeOffset) - last modified timestamp for the blob.</span></span> <span data-ttu-id="08da2-183">Azure Search uses this timestamp to identify changed blobs, to avoid reindexing everything after the initial indexing.</span><span class="sxs-lookup"><span data-stu-id="08da2-183">Azure Search uses this timestamp to identify changed blobs, to avoid reindexing everything after the initial indexing.</span></span>
  * <span data-ttu-id="08da2-184">**metadata\_storage\_size** (Edm.Int64) - blob size in bytes.</span><span class="sxs-lookup"><span data-stu-id="08da2-184">**metadata\_storage\_size** (Edm.Int64) - blob size in bytes.</span></span>
  * <span data-ttu-id="08da2-185">**metadata\_storage\_content\_md5** (Edm.String) - MD5 hash of the blob content, if available.</span><span class="sxs-lookup"><span data-stu-id="08da2-185">**metadata\_storage\_content\_md5** (Edm.String) - MD5 hash of the blob content, if available.</span></span>
* <span data-ttu-id="08da2-186">Metadata properties specific to each document format are extracted into the fields listed [here](#ContentSpecificMetadata).</span><span class="sxs-lookup"><span data-stu-id="08da2-186">Metadata properties specific to each document format are extracted into the fields listed [here](#ContentSpecificMetadata).</span></span>

<span data-ttu-id="08da2-187">You don't need to define fields for all of the above properties in your search index - just capture the properties you need for your application.</span><span class="sxs-lookup"><span data-stu-id="08da2-187">You don't need to define fields for all of the above properties in your search index - just capture the properties you need for your application.</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-188">Often, the field names in your existing index will be different from the field names generated during document extraction.</span><span class="sxs-lookup"><span data-stu-id="08da2-188">Often, the field names in your existing index will be different from the field names generated during document extraction.</span></span> <span data-ttu-id="08da2-189">You can use **field mappings** to map the property names provided by Azure Search to the field names in your search index.</span><span class="sxs-lookup"><span data-stu-id="08da2-189">You can use **field mappings** to map the property names provided by Azure Search to the field names in your search index.</span></span> <span data-ttu-id="08da2-190">You will see an example of field mappings use below.</span><span class="sxs-lookup"><span data-stu-id="08da2-190">You will see an example of field mappings use below.</span></span>
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a><span data-ttu-id="08da2-191">Defining document keys and field mappings</span><span class="sxs-lookup"><span data-stu-id="08da2-191">Defining document keys and field mappings</span></span>
<span data-ttu-id="08da2-192">In Azure Search, the document key uniquely identifies a document.</span><span class="sxs-lookup"><span data-stu-id="08da2-192">In Azure Search, the document key uniquely identifies a document.</span></span> <span data-ttu-id="08da2-193">Every search index must have exactly one key field of type Edm.String.</span><span class="sxs-lookup"><span data-stu-id="08da2-193">Every search index must have exactly one key field of type Edm.String.</span></span> <span data-ttu-id="08da2-194">The key field is required for each document that is being added to the index (it is actually the only required field).</span><span class="sxs-lookup"><span data-stu-id="08da2-194">The key field is required for each document that is being added to the index (it is actually the only required field).</span></span>  

<span data-ttu-id="08da2-195">You should carefully consider which extracted field should map to the key field for your index.</span><span class="sxs-lookup"><span data-stu-id="08da2-195">You should carefully consider which extracted field should map to the key field for your index.</span></span> <span data-ttu-id="08da2-196">The candidates are:</span><span class="sxs-lookup"><span data-stu-id="08da2-196">The candidates are:</span></span>

* <span data-ttu-id="08da2-197">**metadata\_storage\_name** - this might be a convenient candidate, but note that 1) the names might not be unique, as you may have blobs with the same name in different folders, and 2) the name may contain characters that are invalid in document keys, such as dashes.</span><span class="sxs-lookup"><span data-stu-id="08da2-197">**metadata\_storage\_name** - this might be a convenient candidate, but note that 1) the names might not be unique, as you may have blobs with the same name in different folders, and 2) the name may contain characters that are invalid in document keys, such as dashes.</span></span> <span data-ttu-id="08da2-198">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction) - if you do this, remember to encode document keys when passing them in API calls such as Lookup.</span><span class="sxs-lookup"><span data-stu-id="08da2-198">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction) - if you do this, remember to encode document keys when passing them in API calls such as Lookup.</span></span> <span data-ttu-id="08da2-199">(For example, in .NET you can use the [UrlTokenEncode method](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) for that purpose).</span><span class="sxs-lookup"><span data-stu-id="08da2-199">(For example, in .NET you can use the [UrlTokenEncode method](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) for that purpose).</span></span>
* <span data-ttu-id="08da2-200">**metadata\_storage\_path** - using the full path ensures uniqueness, but the path definitely contains `/` characters that are [invalid in a document key](https://docs.microsoft.com/rest/api/searchservice/naming-rules).</span><span class="sxs-lookup"><span data-stu-id="08da2-200">**metadata\_storage\_path** - using the full path ensures uniqueness, but the path definitely contains `/` characters that are [invalid in a document key](https://docs.microsoft.com/rest/api/searchservice/naming-rules).</span></span>  <span data-ttu-id="08da2-201">As above, you have the option of encoding the keys using the `base64Encode` [function](search-indexer-field-mappings.md#base64EncodeFunction).</span><span class="sxs-lookup"><span data-stu-id="08da2-201">As above, you have the option of encoding the keys using the `base64Encode` [function](search-indexer-field-mappings.md#base64EncodeFunction).</span></span>
* <span data-ttu-id="08da2-202">If none of the options above work for you, you can add a custom metadata property to the blobs.</span><span class="sxs-lookup"><span data-stu-id="08da2-202">If none of the options above work for you, you can add a custom metadata property to the blobs.</span></span> <span data-ttu-id="08da2-203">This option does, however, require your blob upload process to add that metadata property to all blobs.</span><span class="sxs-lookup"><span data-stu-id="08da2-203">This option does, however, require your blob upload process to add that metadata property to all blobs.</span></span> <span data-ttu-id="08da2-204">Since the key is a required property, all blobs that don't have that property will fail to be indexed.</span><span class="sxs-lookup"><span data-stu-id="08da2-204">Since the key is a required property, all blobs that don't have that property will fail to be indexed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08da2-205">If there is no explicit mapping for the key field in the index, Azure Search automatically uses `metadata_storage_path` as the key and base-64 encodes key values (the second option above).</span><span class="sxs-lookup"><span data-stu-id="08da2-205">If there is no explicit mapping for the key field in the index, Azure Search automatically uses `metadata_storage_path` as the key and base-64 encodes key values (the second option above).</span></span>
>
>

<span data-ttu-id="08da2-206">For this example, let's pick the `metadata_storage_name` field as the document key.</span><span class="sxs-lookup"><span data-stu-id="08da2-206">For this example, let's pick the `metadata_storage_name` field as the document key.</span></span> <span data-ttu-id="08da2-207">Let's also assume your index has a key field named `key` and a field `fileSize` for storing the document size.</span><span class="sxs-lookup"><span data-stu-id="08da2-207">Let's also assume your index has a key field named `key` and a field `fileSize` for storing the document size.</span></span> <span data-ttu-id="08da2-208">To wire things up as desired, specify the following field mappings when creating or updating your indexer:</span><span class="sxs-lookup"><span data-stu-id="08da2-208">To wire things up as desired, specify the following field mappings when creating or updating your indexer:</span></span>

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

<span data-ttu-id="08da2-209">To bring this all together, here's how you can add field mappings and enable base-64 encoding of keys for an existing indexer:</span><span class="sxs-lookup"><span data-stu-id="08da2-209">To bring this all together, here's how you can add field mappings and enable base-64 encoding of keys for an existing indexer:</span></span>

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> <span data-ttu-id="08da2-210">To learn more about field mappings, see [this article](search-indexer-field-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="08da2-210">To learn more about field mappings, see [this article](search-indexer-field-mappings.md).</span></span>
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a><span data-ttu-id="08da2-211">Controlling which blobs are indexed</span><span class="sxs-lookup"><span data-stu-id="08da2-211">Controlling which blobs are indexed</span></span>
<span data-ttu-id="08da2-212">You can control which blobs are indexed, and which are skipped.</span><span class="sxs-lookup"><span data-stu-id="08da2-212">You can control which blobs are indexed, and which are skipped.</span></span>

### <a name="index-only-the-blobs-with-specific-file-extensions"></a><span data-ttu-id="08da2-213">Index only the blobs with specific file extensions</span><span class="sxs-lookup"><span data-stu-id="08da2-213">Index only the blobs with specific file extensions</span></span>
<span data-ttu-id="08da2-214">You can index only the blobs with the file name extensions you specify by using the `indexedFileNameExtensions` indexer configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="08da2-214">You can index only the blobs with the file name extensions you specify by using the `indexedFileNameExtensions` indexer configuration parameter.</span></span> <span data-ttu-id="08da2-215">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span><span class="sxs-lookup"><span data-stu-id="08da2-215">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span></span> <span data-ttu-id="08da2-216">For example, to index only the .PDF and .DOCX blobs, do this:</span><span class="sxs-lookup"><span data-stu-id="08da2-216">For example, to index only the .PDF and .DOCX blobs, do this:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a><span data-ttu-id="08da2-217">Exclude blobs with specific file extensions</span><span class="sxs-lookup"><span data-stu-id="08da2-217">Exclude blobs with specific file extensions</span></span>
<span data-ttu-id="08da2-218">You can exclude blobs with specific file name extensions from indexing by using the `excludedFileNameExtensions` configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="08da2-218">You can exclude blobs with specific file name extensions from indexing by using the `excludedFileNameExtensions` configuration parameter.</span></span> <span data-ttu-id="08da2-219">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span><span class="sxs-lookup"><span data-stu-id="08da2-219">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span></span> <span data-ttu-id="08da2-220">For example, to index all blobs except those with the .PNG and .JPEG extensions, do this:</span><span class="sxs-lookup"><span data-stu-id="08da2-220">For example, to index all blobs except those with the .PNG and .JPEG extensions, do this:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

<span data-ttu-id="08da2-221">If both `indexedFileNameExtensions` and `excludedFileNameExtensions` parameters are present, Azure Search first looks at `indexedFileNameExtensions`, then at `excludedFileNameExtensions`.</span><span class="sxs-lookup"><span data-stu-id="08da2-221">If both `indexedFileNameExtensions` and `excludedFileNameExtensions` parameters are present, Azure Search first looks at `indexedFileNameExtensions`, then at `excludedFileNameExtensions`.</span></span> <span data-ttu-id="08da2-222">This means that if the same file extension is present in both lists, it will be excluded from indexing.</span><span class="sxs-lookup"><span data-stu-id="08da2-222">This means that if the same file extension is present in both lists, it will be excluded from indexing.</span></span>

### <a name="dealing-with-unsupported-content-types"></a><span data-ttu-id="08da2-223">Dealing with unsupported content types</span><span class="sxs-lookup"><span data-stu-id="08da2-223">Dealing with unsupported content types</span></span>

<span data-ttu-id="08da2-224">By default, the blob indexer stops as soon as it encounters a blob with an unsupported content type (for example, an image).</span><span class="sxs-lookup"><span data-stu-id="08da2-224">By default, the blob indexer stops as soon as it encounters a blob with an unsupported content type (for example, an image).</span></span> <span data-ttu-id="08da2-225">You can of course use the `excludedFileNameExtensions` parameter to skip certain content types.</span><span class="sxs-lookup"><span data-stu-id="08da2-225">You can of course use the `excludedFileNameExtensions` parameter to skip certain content types.</span></span> <span data-ttu-id="08da2-226">However, you may need to index blobs without knowing all the possible content types in advance.</span><span class="sxs-lookup"><span data-stu-id="08da2-226">However, you may need to index blobs without knowing all the possible content types in advance.</span></span> <span data-ttu-id="08da2-227">To continue indexing when an unsupported content type is encountered, set the `failOnUnsupportedContentType` configuration parameter to `false`:</span><span class="sxs-lookup"><span data-stu-id="08da2-227">To continue indexing when an unsupported content type is encountered, set the `failOnUnsupportedContentType` configuration parameter to `false`:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a><span data-ttu-id="08da2-228">Ignoring parsing errors</span><span class="sxs-lookup"><span data-stu-id="08da2-228">Ignoring parsing errors</span></span>

<span data-ttu-id="08da2-229">Azure Search document extraction logic isn't perfect and will sometimes fail to parse documents of a supported content type, such as .DOCX or .PDF.</span><span class="sxs-lookup"><span data-stu-id="08da2-229">Azure Search document extraction logic isn't perfect and will sometimes fail to parse documents of a supported content type, such as .DOCX or .PDF.</span></span> <span data-ttu-id="08da2-230">If you do not want to interrupt the indexing in such cases, set the `maxFailedItems` and `maxFailedItemsPerBatch` configuration parameters to some reasonable values.</span><span class="sxs-lookup"><span data-stu-id="08da2-230">If you do not want to interrupt the indexing in such cases, set the `maxFailedItems` and `maxFailedItemsPerBatch` configuration parameters to some reasonable values.</span></span> <span data-ttu-id="08da2-231">For example:</span><span class="sxs-lookup"><span data-stu-id="08da2-231">For example:</span></span>

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-the-blob-are-indexed"></a><span data-ttu-id="08da2-232">Controlling which parts of the blob are indexed</span><span class="sxs-lookup"><span data-stu-id="08da2-232">Controlling which parts of the blob are indexed</span></span>

<span data-ttu-id="08da2-233">You can control which parts of the blobs are indexed using the `dataToExtract` configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="08da2-233">You can control which parts of the blobs are indexed using the `dataToExtract` configuration parameter.</span></span> <span data-ttu-id="08da2-234">It can take the following values:</span><span class="sxs-lookup"><span data-stu-id="08da2-234">It can take the following values:</span></span>

* <span data-ttu-id="08da2-235">`storageMetadata` - specifies that only the [standard blob properties and user-specified metadata](../storage/storage-properties-metadata.md) are indexed.</span><span class="sxs-lookup"><span data-stu-id="08da2-235">`storageMetadata` - specifies that only the [standard blob properties and user-specified metadata](../storage/storage-properties-metadata.md) are indexed.</span></span>
* <span data-ttu-id="08da2-236">`allMetadata` - specifies that storage metadata and the [content-type specific metadata](#ContentSpecificMetadata) extracted from the blob content are indexed.</span><span class="sxs-lookup"><span data-stu-id="08da2-236">`allMetadata` - specifies that storage metadata and the [content-type specific metadata](#ContentSpecificMetadata) extracted from the blob content are indexed.</span></span>
* <span data-ttu-id="08da2-237">`contentAndMetadata` - specifies that all metadata and textual content extracted from the blob are indexed.</span><span class="sxs-lookup"><span data-stu-id="08da2-237">`contentAndMetadata` - specifies that all metadata and textual content extracted from the blob are indexed.</span></span> <span data-ttu-id="08da2-238">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="08da2-238">This is the default value.</span></span>

<span data-ttu-id="08da2-239">For example, to index only the storage metadata, use:</span><span class="sxs-lookup"><span data-stu-id="08da2-239">For example, to index only the storage metadata, use:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-to-control-how-blobs-are-indexed"></a><span data-ttu-id="08da2-240">Using blob metadata to control how blobs are indexed</span><span class="sxs-lookup"><span data-stu-id="08da2-240">Using blob metadata to control how blobs are indexed</span></span>

<span data-ttu-id="08da2-241">The configuration parameters described above apply to all blobs.</span><span class="sxs-lookup"><span data-stu-id="08da2-241">The configuration parameters described above apply to all blobs.</span></span> <span data-ttu-id="08da2-242">Sometimes, you may want to control how *individual blobs* are indexed.</span><span class="sxs-lookup"><span data-stu-id="08da2-242">Sometimes, you may want to control how *individual blobs* are indexed.</span></span> <span data-ttu-id="08da2-243">You can do this by adding the following blob metadata properties and values:</span><span class="sxs-lookup"><span data-stu-id="08da2-243">You can do this by adding the following blob metadata properties and values:</span></span>

| <span data-ttu-id="08da2-244">Property name</span><span class="sxs-lookup"><span data-stu-id="08da2-244">Property name</span></span> | <span data-ttu-id="08da2-245">Property value</span><span class="sxs-lookup"><span data-stu-id="08da2-245">Property value</span></span> | <span data-ttu-id="08da2-246">Explanation</span><span class="sxs-lookup"><span data-stu-id="08da2-246">Explanation</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08da2-247">AzureSearch_Skip</span><span class="sxs-lookup"><span data-stu-id="08da2-247">AzureSearch_Skip</span></span> |<span data-ttu-id="08da2-248">"true"</span><span class="sxs-lookup"><span data-stu-id="08da2-248">"true"</span></span> |<span data-ttu-id="08da2-249">Instructs the blob indexer to completely skip the blob.</span><span class="sxs-lookup"><span data-stu-id="08da2-249">Instructs the blob indexer to completely skip the blob.</span></span> <span data-ttu-id="08da2-250">Neither metadata nor content extraction is attempted.</span><span class="sxs-lookup"><span data-stu-id="08da2-250">Neither metadata nor content extraction is attempted.</span></span> <span data-ttu-id="08da2-251">This is useful when a particular blob fails repeatedly and interrupts the indexing process.</span><span class="sxs-lookup"><span data-stu-id="08da2-251">This is useful when a particular blob fails repeatedly and interrupts the indexing process.</span></span> |
| <span data-ttu-id="08da2-252">AzureSearch_SkipContent</span><span class="sxs-lookup"><span data-stu-id="08da2-252">AzureSearch_SkipContent</span></span> |<span data-ttu-id="08da2-253">"true"</span><span class="sxs-lookup"><span data-stu-id="08da2-253">"true"</span></span> |<span data-ttu-id="08da2-254">This is equivalent of `"dataToExtract" : "allMetadata"` setting described [above](#PartsOfBlobToIndex) scoped to a particular blob.</span><span class="sxs-lookup"><span data-stu-id="08da2-254">This is equivalent of `"dataToExtract" : "allMetadata"` setting described [above](#PartsOfBlobToIndex) scoped to a particular blob.</span></span> |

## <a name="incremental-indexing-and-deletion-detection"></a><span data-ttu-id="08da2-255">Incremental indexing and deletion detection</span><span class="sxs-lookup"><span data-stu-id="08da2-255">Incremental indexing and deletion detection</span></span>
<span data-ttu-id="08da2-256">When you set up a blob indexer to run on a schedule, it re-indexes only the changed blobs, as determined by the blob's `LastModified` timestamp.</span><span class="sxs-lookup"><span data-stu-id="08da2-256">When you set up a blob indexer to run on a schedule, it re-indexes only the changed blobs, as determined by the blob's `LastModified` timestamp.</span></span>

> [!NOTE]
> <span data-ttu-id="08da2-257">You don't have to specify a change detection policy – incremental indexing is enabled for you automatically.</span><span class="sxs-lookup"><span data-stu-id="08da2-257">You don't have to specify a change detection policy – incremental indexing is enabled for you automatically.</span></span>

<span data-ttu-id="08da2-258">To support deleting documents, use a "soft delete" approach.</span><span class="sxs-lookup"><span data-stu-id="08da2-258">To support deleting documents, use a "soft delete" approach.</span></span> <span data-ttu-id="08da2-259">If you delete the blobs outright, corresponding documents will not be removed from the search index.</span><span class="sxs-lookup"><span data-stu-id="08da2-259">If you delete the blobs outright, corresponding documents will not be removed from the search index.</span></span> <span data-ttu-id="08da2-260">Instead, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="08da2-260">Instead, use the following steps:</span></span>  

1. <span data-ttu-id="08da2-261">Add a custom metadata property to the blob to indicate to Azure Search that it is logically deleted</span><span class="sxs-lookup"><span data-stu-id="08da2-261">Add a custom metadata property to the blob to indicate to Azure Search that it is logically deleted</span></span>
2. <span data-ttu-id="08da2-262">Configure a soft deletion detection policy on the data source</span><span class="sxs-lookup"><span data-stu-id="08da2-262">Configure a soft deletion detection policy on the data source</span></span>
3. <span data-ttu-id="08da2-263">Once the indexer has processed the blob (as shown by the indexer status API), you can physically delete the blob</span><span class="sxs-lookup"><span data-stu-id="08da2-263">Once the indexer has processed the blob (as shown by the indexer status API), you can physically delete the blob</span></span>

<span data-ttu-id="08da2-264">For example, the following policy considers a blob to be deleted if it has a metadata property `IsDeleted` with the value `true`:</span><span class="sxs-lookup"><span data-stu-id="08da2-264">For example, the following policy considers a blob to be deleted if it has a metadata property `IsDeleted` with the value `true`:</span></span>

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a><span data-ttu-id="08da2-265">Indexing large datasets</span><span class="sxs-lookup"><span data-stu-id="08da2-265">Indexing large datasets</span></span>

<span data-ttu-id="08da2-266">Indexing blobs can be a time-consuming process.</span><span class="sxs-lookup"><span data-stu-id="08da2-266">Indexing blobs can be a time-consuming process.</span></span> <span data-ttu-id="08da2-267">In cases where you have millions of blobs to index, you can speed up indexing by partitioning your data and using multiple indexers to process the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="08da2-267">In cases where you have millions of blobs to index, you can speed up indexing by partitioning your data and using multiple indexers to process the data in parallel.</span></span> <span data-ttu-id="08da2-268">Here's how you can set this up:</span><span class="sxs-lookup"><span data-stu-id="08da2-268">Here's how you can set this up:</span></span>

- <span data-ttu-id="08da2-269">Partition your data into multiple blob containers or virtual folders</span><span class="sxs-lookup"><span data-stu-id="08da2-269">Partition your data into multiple blob containers or virtual folders</span></span>
- <span data-ttu-id="08da2-270">Set up several Azure Search data sources, one per container or folder.</span><span class="sxs-lookup"><span data-stu-id="08da2-270">Set up several Azure Search data sources, one per container or folder.</span></span> <span data-ttu-id="08da2-271">To point to a blob folder, use the `query` parameter:</span><span class="sxs-lookup"><span data-stu-id="08da2-271">To point to a blob folder, use the `query` parameter:</span></span>

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- <span data-ttu-id="08da2-272">Create a corresponding indexer for each data source.</span><span class="sxs-lookup"><span data-stu-id="08da2-272">Create a corresponding indexer for each data source.</span></span> <span data-ttu-id="08da2-273">All the indexers can point to the same target search index.</span><span class="sxs-lookup"><span data-stu-id="08da2-273">All the indexers can point to the same target search index.</span></span>  

## <a name="indexing-documents-along-with-related-data"></a><span data-ttu-id="08da2-274">Indexing documents along with related data</span><span class="sxs-lookup"><span data-stu-id="08da2-274">Indexing documents along with related data</span></span>

<span data-ttu-id="08da2-275">Your documents may have associated metadata - for example, the department that created the document - that's stored as structured data in one of the following locations.</span><span class="sxs-lookup"><span data-stu-id="08da2-275">Your documents may have associated metadata - for example, the department that created the document - that's stored as structured data in one of the following locations.</span></span>
-   <span data-ttu-id="08da2-276">In a separate data store, such as SQL Database or DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="08da2-276">In a separate data store, such as SQL Database or DocumentDB.</span></span>
-   <span data-ttu-id="08da2-277">Directly attached to each document in Azure Blob Storage as custom metadata.</span><span class="sxs-lookup"><span data-stu-id="08da2-277">Directly attached to each document in Azure Blob Storage as custom metadata.</span></span> <span data-ttu-id="08da2-278">(For more info, see [Setting and Retrieving Properties and Metadata for Blob Resources](https://docs.microsoft.com/rest/api/storageservices/fileservices/setting-and-retrieving-properties-and-metadata-for-blob-resources).)</span><span class="sxs-lookup"><span data-stu-id="08da2-278">(For more info, see [Setting and Retrieving Properties and Metadata for Blob Resources](https://docs.microsoft.com/rest/api/storageservices/fileservices/setting-and-retrieving-properties-and-metadata-for-blob-resources).)</span></span>

<span data-ttu-id="08da2-279">You can index the documents along with their metadata by assigning the same unique key value to each document and to its metadata, and by specifying the `mergeOrUpload` action for each indexer.</span><span class="sxs-lookup"><span data-stu-id="08da2-279">You can index the documents along with their metadata by assigning the same unique key value to each document and to its metadata, and by specifying the `mergeOrUpload` action for each indexer.</span></span> <span data-ttu-id="08da2-280">For a detailed description of this solution, see this external article: [Combine documents with other data in Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).</span><span class="sxs-lookup"><span data-stu-id="08da2-280">For a detailed description of this solution, see this external article: [Combine documents with other data in Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).</span></span>

<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a><span data-ttu-id="08da2-281">Content type-specific metadata properties</span><span class="sxs-lookup"><span data-stu-id="08da2-281">Content type-specific metadata properties</span></span>
<span data-ttu-id="08da2-282">The following table summarizes processing done for each document format, and describes the metadata properties extracted by Azure Search.</span><span class="sxs-lookup"><span data-stu-id="08da2-282">The following table summarizes processing done for each document format, and describes the metadata properties extracted by Azure Search.</span></span>

| <span data-ttu-id="08da2-283">Document format / content type</span><span class="sxs-lookup"><span data-stu-id="08da2-283">Document format / content type</span></span> | <span data-ttu-id="08da2-284">Content-type specific metadata properties</span><span class="sxs-lookup"><span data-stu-id="08da2-284">Content-type specific metadata properties</span></span> | <span data-ttu-id="08da2-285">Processing details</span><span class="sxs-lookup"><span data-stu-id="08da2-285">Processing details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08da2-286">HTML (`text/html`)</span><span class="sxs-lookup"><span data-stu-id="08da2-286">HTML (`text/html`)</span></span> |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |<span data-ttu-id="08da2-287">Strip HTML markup and extract text</span><span class="sxs-lookup"><span data-stu-id="08da2-287">Strip HTML markup and extract text</span></span> |
| <span data-ttu-id="08da2-288">PDF (`application/pdf`)</span><span class="sxs-lookup"><span data-stu-id="08da2-288">PDF (`application/pdf`)</span></span> |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |<span data-ttu-id="08da2-289">Extract text, including embedded documents (excluding images)</span><span class="sxs-lookup"><span data-stu-id="08da2-289">Extract text, including embedded documents (excluding images)</span></span> |
| <span data-ttu-id="08da2-290">DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document)</span><span class="sxs-lookup"><span data-stu-id="08da2-290">DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |<span data-ttu-id="08da2-291">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-291">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-292">DOC (application/msword)</span><span class="sxs-lookup"><span data-stu-id="08da2-292">DOC (application/msword)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |<span data-ttu-id="08da2-293">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-293">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-294">XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)</span><span class="sxs-lookup"><span data-stu-id="08da2-294">XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |<span data-ttu-id="08da2-295">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-295">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-296">XLS (application/vnd.ms-excel)</span><span class="sxs-lookup"><span data-stu-id="08da2-296">XLS (application/vnd.ms-excel)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |<span data-ttu-id="08da2-297">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-297">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-298">PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation)</span><span class="sxs-lookup"><span data-stu-id="08da2-298">PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |<span data-ttu-id="08da2-299">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-299">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-300">PPT (application/vnd.ms-powerpoint)</span><span class="sxs-lookup"><span data-stu-id="08da2-300">PPT (application/vnd.ms-powerpoint)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |<span data-ttu-id="08da2-301">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="08da2-301">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="08da2-302">MSG (application/vnd.ms-outlook)</span><span class="sxs-lookup"><span data-stu-id="08da2-302">MSG (application/vnd.ms-outlook)</span></span> |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |<span data-ttu-id="08da2-303">Extract text, including attachments</span><span class="sxs-lookup"><span data-stu-id="08da2-303">Extract text, including attachments</span></span> |
| <span data-ttu-id="08da2-304">ZIP (application/zip)</span><span class="sxs-lookup"><span data-stu-id="08da2-304">ZIP (application/zip)</span></span> |`metadata_content_type` |<span data-ttu-id="08da2-305">Extract text from all documents in the archive</span><span class="sxs-lookup"><span data-stu-id="08da2-305">Extract text from all documents in the archive</span></span> |
| <span data-ttu-id="08da2-306">XML (application/xml)</span><span class="sxs-lookup"><span data-stu-id="08da2-306">XML (application/xml)</span></span> |`metadata_content_type`</br>`metadata_content_encoding`</br> |<span data-ttu-id="08da2-307">Strip XML markup and extract text</span><span class="sxs-lookup"><span data-stu-id="08da2-307">Strip XML markup and extract text</span></span> |
| <span data-ttu-id="08da2-308">JSON (application/json)</span><span class="sxs-lookup"><span data-stu-id="08da2-308">JSON (application/json)</span></span> |`metadata_content_type`</br>`metadata_content_encoding` |<span data-ttu-id="08da2-309">Extract text</span><span class="sxs-lookup"><span data-stu-id="08da2-309">Extract text</span></span><br/><span data-ttu-id="08da2-310">NOTE: If you need to extract multiple document fields from a JSON blob, see [Indexing JSON blobs](search-howto-index-json-blobs.md) for details</span><span class="sxs-lookup"><span data-stu-id="08da2-310">NOTE: If you need to extract multiple document fields from a JSON blob, see [Indexing JSON blobs](search-howto-index-json-blobs.md) for details</span></span> |
| <span data-ttu-id="08da2-311">EML (message/rfc822)</span><span class="sxs-lookup"><span data-stu-id="08da2-311">EML (message/rfc822)</span></span> |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |<span data-ttu-id="08da2-312">Extract text, including attachments</span><span class="sxs-lookup"><span data-stu-id="08da2-312">Extract text, including attachments</span></span> |
| <span data-ttu-id="08da2-313">Plain text (text/plain)</span><span class="sxs-lookup"><span data-stu-id="08da2-313">Plain text (text/plain)</span></span> |`metadata_content_type`</br>`metadata_content_encoding`</br> | |

## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="08da2-314">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="08da2-314">Help us make Azure Search better</span></span>
<span data-ttu-id="08da2-315">If you have feature requests or ideas for improvements, let us know on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="08da2-315">If you have feature requests or ideas for improvements, let us know on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
