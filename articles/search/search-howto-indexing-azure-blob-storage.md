---
title: Indexing Azure Blob Storage with Azure Search
description: Learn how to index Azure Blob Storage and extract text from documents with Azure Search
author: chaosrealm
manager: jlembicz
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: eugenesh
ms.openlocfilehash: b2660a98139068a8472c018de5cfbd29d6867c5a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784048"
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a><span data-ttu-id="99255-103">Indexing Documents in Azure Blob Storage with Azure Search</span><span class="sxs-lookup"><span data-stu-id="99255-103">Indexing Documents in Azure Blob Storage with Azure Search</span></span>
<span data-ttu-id="99255-104">This article shows how to use Azure Search to index documents (such as PDFs, Microsoft Office documents, and several other common formats) stored in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="99255-104">This article shows how to use Azure Search to index documents (such as PDFs, Microsoft Office documents, and several other common formats) stored in Azure Blob storage.</span></span> <span data-ttu-id="99255-105">First, it explains the basics of setting up and configuring a blob indexer.</span><span class="sxs-lookup"><span data-stu-id="99255-105">First, it explains the basics of setting up and configuring a blob indexer.</span></span> <span data-ttu-id="99255-106">Then, it offers a deeper exploration of behaviors and scenarios you are likely to encounter.</span><span class="sxs-lookup"><span data-stu-id="99255-106">Then, it offers a deeper exploration of behaviors and scenarios you are likely to encounter.</span></span>

## <a name="supported-document-formats"></a><span data-ttu-id="99255-107">Supported document formats</span><span class="sxs-lookup"><span data-stu-id="99255-107">Supported document formats</span></span>
<span data-ttu-id="99255-108">The blob indexer can extract text from the following document formats:</span><span class="sxs-lookup"><span data-stu-id="99255-108">The blob indexer can extract text from the following document formats:</span></span>

[!INCLUDE [search-blob-data-sources](../../includes/search-blob-data-sources.md)]

## <a name="setting-up-blob-indexing"></a><span data-ttu-id="99255-109">Setting up blob indexing</span><span class="sxs-lookup"><span data-stu-id="99255-109">Setting up blob indexing</span></span>
<span data-ttu-id="99255-110">You can set up an Azure Blob Storage indexer using:</span><span class="sxs-lookup"><span data-stu-id="99255-110">You can set up an Azure Blob Storage indexer using:</span></span>

* [<span data-ttu-id="99255-111">Azure portal</span><span class="sxs-lookup"><span data-stu-id="99255-111">Azure portal</span></span>](https://ms.portal.azure.com)
* <span data-ttu-id="99255-112">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span><span class="sxs-lookup"><span data-stu-id="99255-112">Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)</span></span>
* <span data-ttu-id="99255-113">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span><span class="sxs-lookup"><span data-stu-id="99255-113">Azure Search [.NET SDK](https://aka.ms/search-sdk)</span></span>

> [!NOTE]
> <span data-ttu-id="99255-114">Some features (for example, field mappings) are not yet available in the portal, and have to be used programmatically.</span><span class="sxs-lookup"><span data-stu-id="99255-114">Some features (for example, field mappings) are not yet available in the portal, and have to be used programmatically.</span></span>
>
>

<span data-ttu-id="99255-115">Here, we demonstrate the flow using the REST API.</span><span class="sxs-lookup"><span data-stu-id="99255-115">Here, we demonstrate the flow using the REST API.</span></span>

### <a name="step-1-create-a-data-source"></a><span data-ttu-id="99255-116">Step 1: Create a data source</span><span class="sxs-lookup"><span data-stu-id="99255-116">Step 1: Create a data source</span></span>
<span data-ttu-id="99255-117">A data source specifies which data to index, credentials needed to access the data, and policies to efficiently identify changes in the data (new, modified, or deleted rows).</span><span class="sxs-lookup"><span data-stu-id="99255-117">A data source specifies which data to index, credentials needed to access the data, and policies to efficiently identify changes in the data (new, modified, or deleted rows).</span></span> <span data-ttu-id="99255-118">A data source can be used by multiple indexers in the same search service.</span><span class="sxs-lookup"><span data-stu-id="99255-118">A data source can be used by multiple indexers in the same search service.</span></span>

<span data-ttu-id="99255-119">For blob indexing, the data source must have the following required properties:</span><span class="sxs-lookup"><span data-stu-id="99255-119">For blob indexing, the data source must have the following required properties:</span></span>

* <span data-ttu-id="99255-120">**name** is the unique name of the data source within your search service.</span><span class="sxs-lookup"><span data-stu-id="99255-120">**name** is the unique name of the data source within your search service.</span></span>
* <span data-ttu-id="99255-121">**type** must be `azureblob`.</span><span class="sxs-lookup"><span data-stu-id="99255-121">**type** must be `azureblob`.</span></span>
* <span data-ttu-id="99255-122">**credentials** provides the storage account connection string as the `credentials.connectionString` parameter.</span><span class="sxs-lookup"><span data-stu-id="99255-122">**credentials** provides the storage account connection string as the `credentials.connectionString` parameter.</span></span> <span data-ttu-id="99255-123">See [How to specify credentials](#Credentials) below for details.</span><span class="sxs-lookup"><span data-stu-id="99255-123">See [How to specify credentials](#Credentials) below for details.</span></span>
* <span data-ttu-id="99255-124">**container** specifies a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="99255-124">**container** specifies a container in your storage account.</span></span> <span data-ttu-id="99255-125">By default, all blobs within the container are retrievable.</span><span class="sxs-lookup"><span data-stu-id="99255-125">By default, all blobs within the container are retrievable.</span></span> <span data-ttu-id="99255-126">If you only want to index blobs in a particular virtual directory, you can specify that directory using the optional **query** parameter.</span><span class="sxs-lookup"><span data-stu-id="99255-126">If you only want to index blobs in a particular virtual directory, you can specify that directory using the optional **query** parameter.</span></span>

<span data-ttu-id="99255-127">To create a data source:</span><span class="sxs-lookup"><span data-stu-id="99255-127">To create a data source:</span></span>

    POST https://[service name].search.windows.net/datasources?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

<span data-ttu-id="99255-128">For more on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span><span class="sxs-lookup"><span data-stu-id="99255-128">For more on the Create Datasource API, see [Create Datasource](https://docs.microsoft.com/rest/api/searchservice/create-data-source).</span></span>

<a name="Credentials"></a>
#### <a name="how-to-specify-credentials"></a><span data-ttu-id="99255-129">How to specify credentials</span><span class="sxs-lookup"><span data-stu-id="99255-129">How to specify credentials</span></span> ####

<span data-ttu-id="99255-130">You can provide the credentials for the blob container in one of these ways:</span><span class="sxs-lookup"><span data-stu-id="99255-130">You can provide the credentials for the blob container in one of these ways:</span></span>

- <span data-ttu-id="99255-131">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`.</span><span class="sxs-lookup"><span data-stu-id="99255-131">**Full access storage account connection string**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`.</span></span> <span data-ttu-id="99255-132">You can get the connection string from the Azure portal by navigating to the storage account blade > Settings > Keys (for Classic storage accounts) or Settings > Access keys (for Azure Resource Manager storage accounts).</span><span class="sxs-lookup"><span data-stu-id="99255-132">You can get the connection string from the Azure portal by navigating to the storage account blade > Settings > Keys (for Classic storage accounts) or Settings > Access keys (for Azure Resource Manager storage accounts).</span></span>
- <span data-ttu-id="99255-133">**Storage account shared access signature** (SAS) connection string: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=b&sp=rl` The SAS should have the list and read permissions on containers and objects (blobs in this case).</span><span class="sxs-lookup"><span data-stu-id="99255-133">**Storage account shared access signature** (SAS) connection string: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<the signature>&spr=https&se=<the validity end time>&srt=co&ss=b&sp=rl` The SAS should have the list and read permissions on containers and objects (blobs in this case).</span></span>
-  <span data-ttu-id="99255-134">**Container shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<the signature>&se=<the validity end time>&sp=rl` The SAS should have the list and read permissions on the container.</span><span class="sxs-lookup"><span data-stu-id="99255-134">**Container shared access signature**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<the signature>&se=<the validity end time>&sp=rl` The SAS should have the list and read permissions on the container.</span></span>

<span data-ttu-id="99255-135">For more info on storage shared access signatures, see [Using Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="99255-135">For more info on storage shared access signatures, see [Using Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99255-136">If you use SAS credentials, you will need to update the data source credentials periodically with renewed signatures to prevent their expiration.</span><span class="sxs-lookup"><span data-stu-id="99255-136">If you use SAS credentials, you will need to update the data source credentials periodically with renewed signatures to prevent their expiration.</span></span> <span data-ttu-id="99255-137">If SAS credentials expire, the indexer will fail with an error message similar to `Credentials provided in the connection string are invalid or have expired.`.</span><span class="sxs-lookup"><span data-stu-id="99255-137">If SAS credentials expire, the indexer will fail with an error message similar to `Credentials provided in the connection string are invalid or have expired.`.</span></span>  

### <a name="step-2-create-an-index"></a><span data-ttu-id="99255-138">Step 2: Create an index</span><span class="sxs-lookup"><span data-stu-id="99255-138">Step 2: Create an index</span></span>
<span data-ttu-id="99255-139">The index specifies the fields in a document, attributes, and other constructs that shape the search experience.</span><span class="sxs-lookup"><span data-stu-id="99255-139">The index specifies the fields in a document, attributes, and other constructs that shape the search experience.</span></span>

<span data-ttu-id="99255-140">Here's how to create an index with a searchable `content` field to store the text extracted from blobs:</span><span class="sxs-lookup"><span data-stu-id="99255-140">Here's how to create an index with a searchable `content` field to store the text extracted from blobs:</span></span>   

    POST https://[service name].search.windows.net/indexes?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

<span data-ttu-id="99255-141">For more on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)</span><span class="sxs-lookup"><span data-stu-id="99255-141">For more on creating indexes, see [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)</span></span>

### <a name="step-3-create-an-indexer"></a><span data-ttu-id="99255-142">Step 3: Create an indexer</span><span class="sxs-lookup"><span data-stu-id="99255-142">Step 3: Create an indexer</span></span>
<span data-ttu-id="99255-143">An indexer connects a data source with a target search index, and provides a schedule to automate the data refresh.</span><span class="sxs-lookup"><span data-stu-id="99255-143">An indexer connects a data source with a target search index, and provides a schedule to automate the data refresh.</span></span>

<span data-ttu-id="99255-144">Once the index and data source have been created, you're ready to create the indexer:</span><span class="sxs-lookup"><span data-stu-id="99255-144">Once the index and data source have been created, you're ready to create the indexer:</span></span>

    POST https://[service name].search.windows.net/indexers?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

<span data-ttu-id="99255-145">This indexer will run every two hours (schedule interval is set to "PT2H").</span><span class="sxs-lookup"><span data-stu-id="99255-145">This indexer will run every two hours (schedule interval is set to "PT2H").</span></span> <span data-ttu-id="99255-146">To run an indexer every 30 minutes, set the interval to "PT30M".</span><span class="sxs-lookup"><span data-stu-id="99255-146">To run an indexer every 30 minutes, set the interval to "PT30M".</span></span> <span data-ttu-id="99255-147">The shortest supported interval is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="99255-147">The shortest supported interval is 5 minutes.</span></span> <span data-ttu-id="99255-148">The schedule is optional - if omitted, an indexer runs only once when it's created.</span><span class="sxs-lookup"><span data-stu-id="99255-148">The schedule is optional - if omitted, an indexer runs only once when it's created.</span></span> <span data-ttu-id="99255-149">However, you can run an indexer on-demand at any time.</span><span class="sxs-lookup"><span data-stu-id="99255-149">However, you can run an indexer on-demand at any time.</span></span>   

<span data-ttu-id="99255-150">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span><span class="sxs-lookup"><span data-stu-id="99255-150">For more details on the Create Indexer API, check out [Create Indexer](https://docs.microsoft.com/rest/api/searchservice/create-indexer).</span></span>

## <a name="how-azure-search-indexes-blobs"></a><span data-ttu-id="99255-151">How Azure Search indexes blobs</span><span class="sxs-lookup"><span data-stu-id="99255-151">How Azure Search indexes blobs</span></span>

<span data-ttu-id="99255-152">Depending on the [indexer configuration](#PartsOfBlobToIndex), the blob indexer can index storage metadata only (useful when you only care about the metadata and don't need to index the content of blobs), storage and content metadata, or both metadata and textual content.</span><span class="sxs-lookup"><span data-stu-id="99255-152">Depending on the [indexer configuration](#PartsOfBlobToIndex), the blob indexer can index storage metadata only (useful when you only care about the metadata and don't need to index the content of blobs), storage and content metadata, or both metadata and textual content.</span></span> <span data-ttu-id="99255-153">By default, the indexer extracts both metadata and content.</span><span class="sxs-lookup"><span data-stu-id="99255-153">By default, the indexer extracts both metadata and content.</span></span>

> [!NOTE]
> <span data-ttu-id="99255-154">By default, blobs with structured content such as JSON or CSV are indexed as a single chunk of text.</span><span class="sxs-lookup"><span data-stu-id="99255-154">By default, blobs with structured content such as JSON or CSV are indexed as a single chunk of text.</span></span> <span data-ttu-id="99255-155">If you want to index JSON and CSV blobs in a structured way, see [Indexing JSON blobs](search-howto-index-json-blobs.md) and [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview features.</span><span class="sxs-lookup"><span data-stu-id="99255-155">If you want to index JSON and CSV blobs in a structured way, see [Indexing JSON blobs](search-howto-index-json-blobs.md) and [Indexing CSV blobs](search-howto-index-csv-blobs.md) preview features.</span></span>
>
> <span data-ttu-id="99255-156">A compound or embedded document (such as a ZIP archive or a Word document with embedded Outlook email containing attachments) is also indexed as a single document.</span><span class="sxs-lookup"><span data-stu-id="99255-156">A compound or embedded document (such as a ZIP archive or a Word document with embedded Outlook email containing attachments) is also indexed as a single document.</span></span>

* <span data-ttu-id="99255-157">The textual content of the document is extracted into a string field named `content`.</span><span class="sxs-lookup"><span data-stu-id="99255-157">The textual content of the document is extracted into a string field named `content`.</span></span>

> [!NOTE]
> <span data-ttu-id="99255-158">Azure Search limits how much text it extracts depending on the pricing tier: 32,000 characters for Free tier, 64,000 for Basic, and 4 million for Standard, Standard S2 and Standard S3 tiers.</span><span class="sxs-lookup"><span data-stu-id="99255-158">Azure Search limits how much text it extracts depending on the pricing tier: 32,000 characters for Free tier, 64,000 for Basic, and 4 million for Standard, Standard S2 and Standard S3 tiers.</span></span> <span data-ttu-id="99255-159">A warning is included in the indexer status response for truncated documents.</span><span class="sxs-lookup"><span data-stu-id="99255-159">A warning is included in the indexer status response for truncated documents.</span></span>  

* <span data-ttu-id="99255-160">User-specified metadata properties present on the blob, if any, are extracted verbatim.</span><span class="sxs-lookup"><span data-stu-id="99255-160">User-specified metadata properties present on the blob, if any, are extracted verbatim.</span></span>
* <span data-ttu-id="99255-161">Standard blob metadata properties are extracted into the following fields:</span><span class="sxs-lookup"><span data-stu-id="99255-161">Standard blob metadata properties are extracted into the following fields:</span></span>

  * <span data-ttu-id="99255-162">**metadata\_storage\_name** (Edm.String) - the file name of the blob.</span><span class="sxs-lookup"><span data-stu-id="99255-162">**metadata\_storage\_name** (Edm.String) - the file name of the blob.</span></span> <span data-ttu-id="99255-163">For example, if you have a blob /my-container/my-folder/subfolder/resume.pdf, the value of this field is `resume.pdf`.</span><span class="sxs-lookup"><span data-stu-id="99255-163">For example, if you have a blob /my-container/my-folder/subfolder/resume.pdf, the value of this field is `resume.pdf`.</span></span>
  * <span data-ttu-id="99255-164">**metadata\_storage\_path** (Edm.String) - the full URI of the blob, including the storage account.</span><span class="sxs-lookup"><span data-stu-id="99255-164">**metadata\_storage\_path** (Edm.String) - the full URI of the blob, including the storage account.</span></span> <span data-ttu-id="99255-165">For example, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`</span><span class="sxs-lookup"><span data-stu-id="99255-165">For example, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`</span></span>
  * <span data-ttu-id="99255-166">**metadata\_storage\_content\_type** (Edm.String) - content type as specified by the code you used to upload the blob.</span><span class="sxs-lookup"><span data-stu-id="99255-166">**metadata\_storage\_content\_type** (Edm.String) - content type as specified by the code you used to upload the blob.</span></span> <span data-ttu-id="99255-167">For example, `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="99255-167">For example, `application/octet-stream`.</span></span>
  * <span data-ttu-id="99255-168">**metadata\_storage\_last\_modified** (Edm.DateTimeOffset) - last modified timestamp for the blob.</span><span class="sxs-lookup"><span data-stu-id="99255-168">**metadata\_storage\_last\_modified** (Edm.DateTimeOffset) - last modified timestamp for the blob.</span></span> <span data-ttu-id="99255-169">Azure Search uses this timestamp to identify changed blobs, to avoid reindexing everything after the initial indexing.</span><span class="sxs-lookup"><span data-stu-id="99255-169">Azure Search uses this timestamp to identify changed blobs, to avoid reindexing everything after the initial indexing.</span></span>
  * <span data-ttu-id="99255-170">**metadata\_storage\_size** (Edm.Int64) - blob size in bytes.</span><span class="sxs-lookup"><span data-stu-id="99255-170">**metadata\_storage\_size** (Edm.Int64) - blob size in bytes.</span></span>
  * <span data-ttu-id="99255-171">**metadata\_storage\_content\_md5** (Edm.String) - MD5 hash of the blob content, if available.</span><span class="sxs-lookup"><span data-stu-id="99255-171">**metadata\_storage\_content\_md5** (Edm.String) - MD5 hash of the blob content, if available.</span></span>
* <span data-ttu-id="99255-172">Metadata properties specific to each document format are extracted into the fields listed [here](#ContentSpecificMetadata).</span><span class="sxs-lookup"><span data-stu-id="99255-172">Metadata properties specific to each document format are extracted into the fields listed [here](#ContentSpecificMetadata).</span></span>

<span data-ttu-id="99255-173">You don't need to define fields for all of the above properties in your search index - just capture the properties you need for your application.</span><span class="sxs-lookup"><span data-stu-id="99255-173">You don't need to define fields for all of the above properties in your search index - just capture the properties you need for your application.</span></span>

> [!NOTE]
> <span data-ttu-id="99255-174">Often, the field names in your existing index will be different from the field names generated during document extraction.</span><span class="sxs-lookup"><span data-stu-id="99255-174">Often, the field names in your existing index will be different from the field names generated during document extraction.</span></span> <span data-ttu-id="99255-175">You can use **field mappings** to map the property names provided by Azure Search to the field names in your search index.</span><span class="sxs-lookup"><span data-stu-id="99255-175">You can use **field mappings** to map the property names provided by Azure Search to the field names in your search index.</span></span> <span data-ttu-id="99255-176">You will see an example of field mappings use below.</span><span class="sxs-lookup"><span data-stu-id="99255-176">You will see an example of field mappings use below.</span></span>
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a><span data-ttu-id="99255-177">Defining document keys and field mappings</span><span class="sxs-lookup"><span data-stu-id="99255-177">Defining document keys and field mappings</span></span>
<span data-ttu-id="99255-178">In Azure Search, the document key uniquely identifies a document.</span><span class="sxs-lookup"><span data-stu-id="99255-178">In Azure Search, the document key uniquely identifies a document.</span></span> <span data-ttu-id="99255-179">Every search index must have exactly one key field of type Edm.String.</span><span class="sxs-lookup"><span data-stu-id="99255-179">Every search index must have exactly one key field of type Edm.String.</span></span> <span data-ttu-id="99255-180">The key field is required for each document that is being added to the index (it is actually the only required field).</span><span class="sxs-lookup"><span data-stu-id="99255-180">The key field is required for each document that is being added to the index (it is actually the only required field).</span></span>  

<span data-ttu-id="99255-181">You should carefully consider which extracted field should map to the key field for your index.</span><span class="sxs-lookup"><span data-stu-id="99255-181">You should carefully consider which extracted field should map to the key field for your index.</span></span> <span data-ttu-id="99255-182">The candidates are:</span><span class="sxs-lookup"><span data-stu-id="99255-182">The candidates are:</span></span>

* <span data-ttu-id="99255-183">**metadata\_storage\_name** - this might be a convenient candidate, but note that 1) the names might not be unique, as you may have blobs with the same name in different folders, and 2) the name may contain characters that are invalid in document keys, such as dashes.</span><span class="sxs-lookup"><span data-stu-id="99255-183">**metadata\_storage\_name** - this might be a convenient candidate, but note that 1) the names might not be unique, as you may have blobs with the same name in different folders, and 2) the name may contain characters that are invalid in document keys, such as dashes.</span></span> <span data-ttu-id="99255-184">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction) - if you do this, remember to encode document keys when passing them in API calls such as Lookup.</span><span class="sxs-lookup"><span data-stu-id="99255-184">You can deal with invalid characters by using the `base64Encode` [field mapping function](search-indexer-field-mappings.md#base64EncodeFunction) - if you do this, remember to encode document keys when passing them in API calls such as Lookup.</span></span> <span data-ttu-id="99255-185">(For example, in .NET you can use the [UrlTokenEncode method](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) for that purpose).</span><span class="sxs-lookup"><span data-stu-id="99255-185">(For example, in .NET you can use the [UrlTokenEncode method](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) for that purpose).</span></span>
* <span data-ttu-id="99255-186">**metadata\_storage\_path** - using the full path ensures uniqueness, but the path definitely contains `/` characters that are [invalid in a document key](https://docs.microsoft.com/rest/api/searchservice/naming-rules).</span><span class="sxs-lookup"><span data-stu-id="99255-186">**metadata\_storage\_path** - using the full path ensures uniqueness, but the path definitely contains `/` characters that are [invalid in a document key](https://docs.microsoft.com/rest/api/searchservice/naming-rules).</span></span>  <span data-ttu-id="99255-187">As above, you have the option of encoding the keys using the `base64Encode` [function](search-indexer-field-mappings.md#base64EncodeFunction).</span><span class="sxs-lookup"><span data-stu-id="99255-187">As above, you have the option of encoding the keys using the `base64Encode` [function](search-indexer-field-mappings.md#base64EncodeFunction).</span></span>
* <span data-ttu-id="99255-188">If none of the options above work for you, you can add a custom metadata property to the blobs.</span><span class="sxs-lookup"><span data-stu-id="99255-188">If none of the options above work for you, you can add a custom metadata property to the blobs.</span></span> <span data-ttu-id="99255-189">This option does, however, require your blob upload process to add that metadata property to all blobs.</span><span class="sxs-lookup"><span data-stu-id="99255-189">This option does, however, require your blob upload process to add that metadata property to all blobs.</span></span> <span data-ttu-id="99255-190">Since the key is a required property, all blobs that don't have that property will fail to be indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-190">Since the key is a required property, all blobs that don't have that property will fail to be indexed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99255-191">If there is no explicit mapping for the key field in the index, Azure Search automatically uses `metadata_storage_path` as the key and base-64 encodes key values (the second option above).</span><span class="sxs-lookup"><span data-stu-id="99255-191">If there is no explicit mapping for the key field in the index, Azure Search automatically uses `metadata_storage_path` as the key and base-64 encodes key values (the second option above).</span></span>
>
>

<span data-ttu-id="99255-192">For this example, let's pick the `metadata_storage_name` field as the document key.</span><span class="sxs-lookup"><span data-stu-id="99255-192">For this example, let's pick the `metadata_storage_name` field as the document key.</span></span> <span data-ttu-id="99255-193">Let's also assume your index has a key field named `key` and a field `fileSize` for storing the document size.</span><span class="sxs-lookup"><span data-stu-id="99255-193">Let's also assume your index has a key field named `key` and a field `fileSize` for storing the document size.</span></span> <span data-ttu-id="99255-194">To wire things up as desired, specify the following field mappings when creating or updating your indexer:</span><span class="sxs-lookup"><span data-stu-id="99255-194">To wire things up as desired, specify the following field mappings when creating or updating your indexer:</span></span>

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

<span data-ttu-id="99255-195">To bring this all together, here's how you can add field mappings and enable base-64 encoding of keys for an existing indexer:</span><span class="sxs-lookup"><span data-stu-id="99255-195">To bring this all together, here's how you can add field mappings and enable base-64 encoding of keys for an existing indexer:</span></span>

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2017-11-11
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
> <span data-ttu-id="99255-196">To learn more about field mappings, see [this article](search-indexer-field-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="99255-196">To learn more about field mappings, see [this article](search-indexer-field-mappings.md).</span></span>
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a><span data-ttu-id="99255-197">Controlling which blobs are indexed</span><span class="sxs-lookup"><span data-stu-id="99255-197">Controlling which blobs are indexed</span></span>
<span data-ttu-id="99255-198">You can control which blobs are indexed, and which are skipped.</span><span class="sxs-lookup"><span data-stu-id="99255-198">You can control which blobs are indexed, and which are skipped.</span></span>

### <a name="index-only-the-blobs-with-specific-file-extensions"></a><span data-ttu-id="99255-199">Index only the blobs with specific file extensions</span><span class="sxs-lookup"><span data-stu-id="99255-199">Index only the blobs with specific file extensions</span></span>
<span data-ttu-id="99255-200">You can index only the blobs with the file name extensions you specify by using the `indexedFileNameExtensions` indexer configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="99255-200">You can index only the blobs with the file name extensions you specify by using the `indexedFileNameExtensions` indexer configuration parameter.</span></span> <span data-ttu-id="99255-201">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span><span class="sxs-lookup"><span data-stu-id="99255-201">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span></span> <span data-ttu-id="99255-202">For example, to index only the .PDF and .DOCX blobs, do this:</span><span class="sxs-lookup"><span data-stu-id="99255-202">For example, to index only the .PDF and .DOCX blobs, do this:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a><span data-ttu-id="99255-203">Exclude blobs with specific file extensions</span><span class="sxs-lookup"><span data-stu-id="99255-203">Exclude blobs with specific file extensions</span></span>
<span data-ttu-id="99255-204">You can exclude blobs with specific file name extensions from indexing by using the `excludedFileNameExtensions` configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="99255-204">You can exclude blobs with specific file name extensions from indexing by using the `excludedFileNameExtensions` configuration parameter.</span></span> <span data-ttu-id="99255-205">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span><span class="sxs-lookup"><span data-stu-id="99255-205">The value is a string containing a comma-separated list of file extensions (with a leading dot).</span></span> <span data-ttu-id="99255-206">For example, to index all blobs except those with the .PNG and .JPEG extensions, do this:</span><span class="sxs-lookup"><span data-stu-id="99255-206">For example, to index all blobs except those with the .PNG and .JPEG extensions, do this:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

<span data-ttu-id="99255-207">If both `indexedFileNameExtensions` and `excludedFileNameExtensions` parameters are present, Azure Search first looks at `indexedFileNameExtensions`, then at `excludedFileNameExtensions`.</span><span class="sxs-lookup"><span data-stu-id="99255-207">If both `indexedFileNameExtensions` and `excludedFileNameExtensions` parameters are present, Azure Search first looks at `indexedFileNameExtensions`, then at `excludedFileNameExtensions`.</span></span> <span data-ttu-id="99255-208">This means that if the same file extension is present in both lists, it will be excluded from indexing.</span><span class="sxs-lookup"><span data-stu-id="99255-208">This means that if the same file extension is present in both lists, it will be excluded from indexing.</span></span>

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-the-blob-are-indexed"></a><span data-ttu-id="99255-209">Controlling which parts of the blob are indexed</span><span class="sxs-lookup"><span data-stu-id="99255-209">Controlling which parts of the blob are indexed</span></span>

<span data-ttu-id="99255-210">You can control which parts of the blobs are indexed using the `dataToExtract` configuration parameter.</span><span class="sxs-lookup"><span data-stu-id="99255-210">You can control which parts of the blobs are indexed using the `dataToExtract` configuration parameter.</span></span> <span data-ttu-id="99255-211">It can take the following values:</span><span class="sxs-lookup"><span data-stu-id="99255-211">It can take the following values:</span></span>

* <span data-ttu-id="99255-212">`storageMetadata` - specifies that only the [standard blob properties and user-specified metadata](../storage/blobs/storage-properties-metadata.md) are indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-212">`storageMetadata` - specifies that only the [standard blob properties and user-specified metadata](../storage/blobs/storage-properties-metadata.md) are indexed.</span></span>
* <span data-ttu-id="99255-213">`allMetadata` - specifies that storage metadata and the [content-type specific metadata](#ContentSpecificMetadata) extracted from the blob content are indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-213">`allMetadata` - specifies that storage metadata and the [content-type specific metadata](#ContentSpecificMetadata) extracted from the blob content are indexed.</span></span>
* <span data-ttu-id="99255-214">`contentAndMetadata` - specifies that all metadata and textual content extracted from the blob are indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-214">`contentAndMetadata` - specifies that all metadata and textual content extracted from the blob are indexed.</span></span> <span data-ttu-id="99255-215">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="99255-215">This is the default value.</span></span>

<span data-ttu-id="99255-216">For example, to index only the storage metadata, use:</span><span class="sxs-lookup"><span data-stu-id="99255-216">For example, to index only the storage metadata, use:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-to-control-how-blobs-are-indexed"></a><span data-ttu-id="99255-217">Using blob metadata to control how blobs are indexed</span><span class="sxs-lookup"><span data-stu-id="99255-217">Using blob metadata to control how blobs are indexed</span></span>

<span data-ttu-id="99255-218">The configuration parameters described above apply to all blobs.</span><span class="sxs-lookup"><span data-stu-id="99255-218">The configuration parameters described above apply to all blobs.</span></span> <span data-ttu-id="99255-219">Sometimes, you may want to control how *individual blobs* are indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-219">Sometimes, you may want to control how *individual blobs* are indexed.</span></span> <span data-ttu-id="99255-220">You can do this by adding the following blob metadata properties and values:</span><span class="sxs-lookup"><span data-stu-id="99255-220">You can do this by adding the following blob metadata properties and values:</span></span>

| <span data-ttu-id="99255-221">Property name</span><span class="sxs-lookup"><span data-stu-id="99255-221">Property name</span></span> | <span data-ttu-id="99255-222">Property value</span><span class="sxs-lookup"><span data-stu-id="99255-222">Property value</span></span> | <span data-ttu-id="99255-223">Explanation</span><span class="sxs-lookup"><span data-stu-id="99255-223">Explanation</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99255-224">AzureSearch_Skip</span><span class="sxs-lookup"><span data-stu-id="99255-224">AzureSearch_Skip</span></span> |<span data-ttu-id="99255-225">"true"</span><span class="sxs-lookup"><span data-stu-id="99255-225">"true"</span></span> |<span data-ttu-id="99255-226">Instructs the blob indexer to completely skip the blob.</span><span class="sxs-lookup"><span data-stu-id="99255-226">Instructs the blob indexer to completely skip the blob.</span></span> <span data-ttu-id="99255-227">Neither metadata nor content extraction is attempted.</span><span class="sxs-lookup"><span data-stu-id="99255-227">Neither metadata nor content extraction is attempted.</span></span> <span data-ttu-id="99255-228">This is useful when a particular blob fails repeatedly and interrupts the indexing process.</span><span class="sxs-lookup"><span data-stu-id="99255-228">This is useful when a particular blob fails repeatedly and interrupts the indexing process.</span></span> |
| <span data-ttu-id="99255-229">AzureSearch_SkipContent</span><span class="sxs-lookup"><span data-stu-id="99255-229">AzureSearch_SkipContent</span></span> |<span data-ttu-id="99255-230">"true"</span><span class="sxs-lookup"><span data-stu-id="99255-230">"true"</span></span> |<span data-ttu-id="99255-231">This is equivalent of `"dataToExtract" : "allMetadata"` setting described [above](#PartsOfBlobToIndex) scoped to a particular blob.</span><span class="sxs-lookup"><span data-stu-id="99255-231">This is equivalent of `"dataToExtract" : "allMetadata"` setting described [above](#PartsOfBlobToIndex) scoped to a particular blob.</span></span> |

<a name="DealingWithErrors"></a>
## <a name="dealing-with-errors"></a><span data-ttu-id="99255-232">Dealing with errors</span><span class="sxs-lookup"><span data-stu-id="99255-232">Dealing with errors</span></span>

<span data-ttu-id="99255-233">By default, the blob indexer stops as soon as it encounters a blob with an unsupported content type (for example, an image).</span><span class="sxs-lookup"><span data-stu-id="99255-233">By default, the blob indexer stops as soon as it encounters a blob with an unsupported content type (for example, an image).</span></span> <span data-ttu-id="99255-234">You can of course use the `excludedFileNameExtensions` parameter to skip certain content types.</span><span class="sxs-lookup"><span data-stu-id="99255-234">You can of course use the `excludedFileNameExtensions` parameter to skip certain content types.</span></span> <span data-ttu-id="99255-235">However, you may need to index blobs without knowing all the possible content types in advance.</span><span class="sxs-lookup"><span data-stu-id="99255-235">However, you may need to index blobs without knowing all the possible content types in advance.</span></span> <span data-ttu-id="99255-236">To continue indexing when an unsupported content type is encountered, set the `failOnUnsupportedContentType` configuration parameter to `false`:</span><span class="sxs-lookup"><span data-stu-id="99255-236">To continue indexing when an unsupported content type is encountered, set the `failOnUnsupportedContentType` configuration parameter to `false`:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

<span data-ttu-id="99255-237">For some blobs, Azure Search is unable to determine the content type, or unable to process a document of otherwise supported content type.</span><span class="sxs-lookup"><span data-stu-id="99255-237">For some blobs, Azure Search is unable to determine the content type, or unable to process a document of otherwise supported content type.</span></span> <span data-ttu-id="99255-238">To ignore this failure mode, set the `failOnUnprocessableDocument` configuration parameter to false:</span><span class="sxs-lookup"><span data-stu-id="99255-238">To ignore this failure mode, set the `failOnUnprocessableDocument` configuration parameter to false:</span></span>

      "parameters" : { "configuration" : { "failOnUnprocessableDocument" : false } }

<span data-ttu-id="99255-239">Azure Search limits the size of blobs that are indexed.</span><span class="sxs-lookup"><span data-stu-id="99255-239">Azure Search limits the size of blobs that are indexed.</span></span> <span data-ttu-id="99255-240">These limits are documented in [Service Limits in Azure Search](https://docs.microsoft.com/azure/search/search-limits-quotas-capacity).</span><span class="sxs-lookup"><span data-stu-id="99255-240">These limits are documented in [Service Limits in Azure Search](https://docs.microsoft.com/azure/search/search-limits-quotas-capacity).</span></span> <span data-ttu-id="99255-241">Oversized blobs are treated as errors by default.</span><span class="sxs-lookup"><span data-stu-id="99255-241">Oversized blobs are treated as errors by default.</span></span> <span data-ttu-id="99255-242">However, you can still index storage metadata of oversized blobs if you set `indexStorageMetadataOnlyForOversizedDocuments` configuration parameter to true:</span><span class="sxs-lookup"><span data-stu-id="99255-242">However, you can still index storage metadata of oversized blobs if you set `indexStorageMetadataOnlyForOversizedDocuments` configuration parameter to true:</span></span> 

    "parameters" : { "configuration" : { "indexStorageMetadataOnlyForOversizedDocuments" : true } }

<span data-ttu-id="99255-243">You can also continue indexing if errors happen at any point of processing, either while parsing blobs or while adding documents to an index.</span><span class="sxs-lookup"><span data-stu-id="99255-243">You can also continue indexing if errors happen at any point of processing, either while parsing blobs or while adding documents to an index.</span></span> <span data-ttu-id="99255-244">To ignore a specific number of errors, set the `maxFailedItems` and `maxFailedItemsPerBatch` configuration parameters to the desired values.</span><span class="sxs-lookup"><span data-stu-id="99255-244">To ignore a specific number of errors, set the `maxFailedItems` and `maxFailedItemsPerBatch` configuration parameters to the desired values.</span></span> <span data-ttu-id="99255-245">For example:</span><span class="sxs-lookup"><span data-stu-id="99255-245">For example:</span></span>

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

## <a name="incremental-indexing-and-deletion-detection"></a><span data-ttu-id="99255-246">Incremental indexing and deletion detection</span><span class="sxs-lookup"><span data-stu-id="99255-246">Incremental indexing and deletion detection</span></span>
<span data-ttu-id="99255-247">When you set up a blob indexer to run on a schedule, it reindexes only the changed blobs, as determined by the blob's `LastModified` timestamp.</span><span class="sxs-lookup"><span data-stu-id="99255-247">When you set up a blob indexer to run on a schedule, it reindexes only the changed blobs, as determined by the blob's `LastModified` timestamp.</span></span>

> [!NOTE]
> <span data-ttu-id="99255-248">You don't have to specify a change detection policy – incremental indexing is enabled for you automatically.</span><span class="sxs-lookup"><span data-stu-id="99255-248">You don't have to specify a change detection policy – incremental indexing is enabled for you automatically.</span></span>

<span data-ttu-id="99255-249">To support deleting documents, use a "soft delete" approach.</span><span class="sxs-lookup"><span data-stu-id="99255-249">To support deleting documents, use a "soft delete" approach.</span></span> <span data-ttu-id="99255-250">If you delete the blobs outright, corresponding documents will not be removed from the search index.</span><span class="sxs-lookup"><span data-stu-id="99255-250">If you delete the blobs outright, corresponding documents will not be removed from the search index.</span></span> <span data-ttu-id="99255-251">Instead, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="99255-251">Instead, use the following steps:</span></span>  

1. <span data-ttu-id="99255-252">Add a custom metadata property to the blob to indicate to Azure Search that it is logically deleted</span><span class="sxs-lookup"><span data-stu-id="99255-252">Add a custom metadata property to the blob to indicate to Azure Search that it is logically deleted</span></span>
2. <span data-ttu-id="99255-253">Configure a soft deletion detection policy on the data source</span><span class="sxs-lookup"><span data-stu-id="99255-253">Configure a soft deletion detection policy on the data source</span></span>
3. <span data-ttu-id="99255-254">Once the indexer has processed the blob (as shown by the indexer status API), you can physically delete the blob</span><span class="sxs-lookup"><span data-stu-id="99255-254">Once the indexer has processed the blob (as shown by the indexer status API), you can physically delete the blob</span></span>

<span data-ttu-id="99255-255">For example, the following policy considers a blob to be deleted if it has a metadata property `IsDeleted` with the value `true`:</span><span class="sxs-lookup"><span data-stu-id="99255-255">For example, the following policy considers a blob to be deleted if it has a metadata property `IsDeleted` with the value `true`:</span></span>

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2017-11-11
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

## <a name="indexing-large-datasets"></a><span data-ttu-id="99255-256">Indexing large datasets</span><span class="sxs-lookup"><span data-stu-id="99255-256">Indexing large datasets</span></span>

<span data-ttu-id="99255-257">Indexing blobs can be a time-consuming process.</span><span class="sxs-lookup"><span data-stu-id="99255-257">Indexing blobs can be a time-consuming process.</span></span> <span data-ttu-id="99255-258">In cases where you have millions of blobs to index, you can speed up indexing by partitioning your data and using multiple indexers to process the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="99255-258">In cases where you have millions of blobs to index, you can speed up indexing by partitioning your data and using multiple indexers to process the data in parallel.</span></span> <span data-ttu-id="99255-259">Here's how you can set this up:</span><span class="sxs-lookup"><span data-stu-id="99255-259">Here's how you can set this up:</span></span>

- <span data-ttu-id="99255-260">Partition your data into multiple blob containers or virtual folders</span><span class="sxs-lookup"><span data-stu-id="99255-260">Partition your data into multiple blob containers or virtual folders</span></span>
- <span data-ttu-id="99255-261">Set up several Azure Search data sources, one per container or folder.</span><span class="sxs-lookup"><span data-stu-id="99255-261">Set up several Azure Search data sources, one per container or folder.</span></span> <span data-ttu-id="99255-262">To point to a blob folder, use the `query` parameter:</span><span class="sxs-lookup"><span data-stu-id="99255-262">To point to a blob folder, use the `query` parameter:</span></span>

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- <span data-ttu-id="99255-263">Create a corresponding indexer for each data source.</span><span class="sxs-lookup"><span data-stu-id="99255-263">Create a corresponding indexer for each data source.</span></span> <span data-ttu-id="99255-264">All the indexers can point to the same target search index.</span><span class="sxs-lookup"><span data-stu-id="99255-264">All the indexers can point to the same target search index.</span></span>  

- <span data-ttu-id="99255-265">One search unit in your service can run one indexer at any given time.</span><span class="sxs-lookup"><span data-stu-id="99255-265">One search unit in your service can run one indexer at any given time.</span></span> <span data-ttu-id="99255-266">Creating multiple indexers as described above is only useful if they actually run in parallel.</span><span class="sxs-lookup"><span data-stu-id="99255-266">Creating multiple indexers as described above is only useful if they actually run in parallel.</span></span> <span data-ttu-id="99255-267">To run multiple indexers in parallel, scale out your search service by creating an appropriate number of partitions and replicas.</span><span class="sxs-lookup"><span data-stu-id="99255-267">To run multiple indexers in parallel, scale out your search service by creating an appropriate number of partitions and replicas.</span></span> <span data-ttu-id="99255-268">For example, if your search service has 6 search units (for example, 2 partitions x 3 replicas), then 6 indexers can run simultaneously, resulting in a six-fold increase in the indexing throughput.</span><span class="sxs-lookup"><span data-stu-id="99255-268">For example, if your search service has 6 search units (for example, 2 partitions x 3 replicas), then 6 indexers can run simultaneously, resulting in a six-fold increase in the indexing throughput.</span></span> <span data-ttu-id="99255-269">To learn more about scaling and capacity planning, see [Scale resource levels for query and indexing workloads in Azure Search](search-capacity-planning.md).</span><span class="sxs-lookup"><span data-stu-id="99255-269">To learn more about scaling and capacity planning, see [Scale resource levels for query and indexing workloads in Azure Search](search-capacity-planning.md).</span></span>

## <a name="indexing-documents-along-with-related-data"></a><span data-ttu-id="99255-270">Indexing documents along with related data</span><span class="sxs-lookup"><span data-stu-id="99255-270">Indexing documents along with related data</span></span>

<span data-ttu-id="99255-271">You may want to "assemble" documents from multiple sources in your index.</span><span class="sxs-lookup"><span data-stu-id="99255-271">You may want to "assemble" documents from multiple sources in your index.</span></span> <span data-ttu-id="99255-272">For example, you may want to merge text from blobs with other metadata stored in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="99255-272">For example, you may want to merge text from blobs with other metadata stored in Cosmos DB.</span></span> <span data-ttu-id="99255-273">You can even use the push indexing API together with various indexers to  build up search documents from multiple parts.</span><span class="sxs-lookup"><span data-stu-id="99255-273">You can even use the push indexing API together with various indexers to  build up search documents from multiple parts.</span></span> 

<span data-ttu-id="99255-274">For this to work, all indexers and other components need to agree on the document key.</span><span class="sxs-lookup"><span data-stu-id="99255-274">For this to work, all indexers and other components need to agree on the document key.</span></span> <span data-ttu-id="99255-275">For a detailed walk-through, see this external article: [Combine documents with other data in Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).</span><span class="sxs-lookup"><span data-stu-id="99255-275">For a detailed walk-through, see this external article: [Combine documents with other data in Azure Search ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).</span></span>

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a><span data-ttu-id="99255-276">Indexing plain text</span><span class="sxs-lookup"><span data-stu-id="99255-276">Indexing plain text</span></span> 

<span data-ttu-id="99255-277">If all your blobs contain plain text in the same encoding, you can significantly improve indexing performance by using **text parsing mode**.</span><span class="sxs-lookup"><span data-stu-id="99255-277">If all your blobs contain plain text in the same encoding, you can significantly improve indexing performance by using **text parsing mode**.</span></span> <span data-ttu-id="99255-278">To use text parsing mode, set the `parsingMode` configuration property to `text`:</span><span class="sxs-lookup"><span data-stu-id="99255-278">To use text parsing mode, set the `parsingMode` configuration property to `text`:</span></span>

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2017-11-11
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

<span data-ttu-id="99255-279">By default, the `UTF-8` encoding is assumed.</span><span class="sxs-lookup"><span data-stu-id="99255-279">By default, the `UTF-8` encoding is assumed.</span></span> <span data-ttu-id="99255-280">To specify a different encoding, use the `encoding` configuration property:</span><span class="sxs-lookup"><span data-stu-id="99255-280">To specify a different encoding, use the `encoding` configuration property:</span></span> 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a><span data-ttu-id="99255-281">Content type-specific metadata properties</span><span class="sxs-lookup"><span data-stu-id="99255-281">Content type-specific metadata properties</span></span>
<span data-ttu-id="99255-282">The following table summarizes processing done for each document format, and describes the metadata properties extracted by Azure Search.</span><span class="sxs-lookup"><span data-stu-id="99255-282">The following table summarizes processing done for each document format, and describes the metadata properties extracted by Azure Search.</span></span>

| <span data-ttu-id="99255-283">Document format / content type</span><span class="sxs-lookup"><span data-stu-id="99255-283">Document format / content type</span></span> | <span data-ttu-id="99255-284">Content-type specific metadata properties</span><span class="sxs-lookup"><span data-stu-id="99255-284">Content-type specific metadata properties</span></span> | <span data-ttu-id="99255-285">Processing details</span><span class="sxs-lookup"><span data-stu-id="99255-285">Processing details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99255-286">HTML (`text/html`)</span><span class="sxs-lookup"><span data-stu-id="99255-286">HTML (`text/html`)</span></span> |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |<span data-ttu-id="99255-287">Strip HTML markup and extract text</span><span class="sxs-lookup"><span data-stu-id="99255-287">Strip HTML markup and extract text</span></span> |
| <span data-ttu-id="99255-288">PDF (`application/pdf`)</span><span class="sxs-lookup"><span data-stu-id="99255-288">PDF (`application/pdf`)</span></span> |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |<span data-ttu-id="99255-289">Extract text, including embedded documents (excluding images)</span><span class="sxs-lookup"><span data-stu-id="99255-289">Extract text, including embedded documents (excluding images)</span></span> |
| <span data-ttu-id="99255-290">DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document)</span><span class="sxs-lookup"><span data-stu-id="99255-290">DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |<span data-ttu-id="99255-291">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-291">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-292">DOC (application/msword)</span><span class="sxs-lookup"><span data-stu-id="99255-292">DOC (application/msword)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |<span data-ttu-id="99255-293">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-293">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-294">XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)</span><span class="sxs-lookup"><span data-stu-id="99255-294">XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |<span data-ttu-id="99255-295">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-295">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-296">XLS (application/vnd.ms-excel)</span><span class="sxs-lookup"><span data-stu-id="99255-296">XLS (application/vnd.ms-excel)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |<span data-ttu-id="99255-297">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-297">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-298">PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation)</span><span class="sxs-lookup"><span data-stu-id="99255-298">PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |<span data-ttu-id="99255-299">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-299">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-300">PPT (application/vnd.ms-powerpoint)</span><span class="sxs-lookup"><span data-stu-id="99255-300">PPT (application/vnd.ms-powerpoint)</span></span> |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |<span data-ttu-id="99255-301">Extract text, including embedded documents</span><span class="sxs-lookup"><span data-stu-id="99255-301">Extract text, including embedded documents</span></span> |
| <span data-ttu-id="99255-302">MSG (application/vnd.ms-outlook)</span><span class="sxs-lookup"><span data-stu-id="99255-302">MSG (application/vnd.ms-outlook)</span></span> |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |<span data-ttu-id="99255-303">Extract text, including attachments</span><span class="sxs-lookup"><span data-stu-id="99255-303">Extract text, including attachments</span></span> |
| <span data-ttu-id="99255-304">ZIP (application/zip)</span><span class="sxs-lookup"><span data-stu-id="99255-304">ZIP (application/zip)</span></span> |`metadata_content_type` |<span data-ttu-id="99255-305">Extract text from all documents in the archive</span><span class="sxs-lookup"><span data-stu-id="99255-305">Extract text from all documents in the archive</span></span> |
| <span data-ttu-id="99255-306">XML (application/xml)</span><span class="sxs-lookup"><span data-stu-id="99255-306">XML (application/xml)</span></span> |`metadata_content_type`</br>`metadata_content_encoding`</br> |<span data-ttu-id="99255-307">Strip XML markup and extract text</span><span class="sxs-lookup"><span data-stu-id="99255-307">Strip XML markup and extract text</span></span> |
| <span data-ttu-id="99255-308">JSON (application/json)</span><span class="sxs-lookup"><span data-stu-id="99255-308">JSON (application/json)</span></span> |`metadata_content_type`</br>`metadata_content_encoding` |<span data-ttu-id="99255-309">Extract text</span><span class="sxs-lookup"><span data-stu-id="99255-309">Extract text</span></span><br/><span data-ttu-id="99255-310">NOTE: If you need to extract multiple document fields from a JSON blob, see [Indexing JSON blobs](search-howto-index-json-blobs.md) for details</span><span class="sxs-lookup"><span data-stu-id="99255-310">NOTE: If you need to extract multiple document fields from a JSON blob, see [Indexing JSON blobs](search-howto-index-json-blobs.md) for details</span></span> |
| <span data-ttu-id="99255-311">EML (message/rfc822)</span><span class="sxs-lookup"><span data-stu-id="99255-311">EML (message/rfc822)</span></span> |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |<span data-ttu-id="99255-312">Extract text, including attachments</span><span class="sxs-lookup"><span data-stu-id="99255-312">Extract text, including attachments</span></span> |
| <span data-ttu-id="99255-313">RTF (application/rtf)</span><span class="sxs-lookup"><span data-stu-id="99255-313">RTF (application/rtf)</span></span> |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | <span data-ttu-id="99255-314">Extract text</span><span class="sxs-lookup"><span data-stu-id="99255-314">Extract text</span></span>|
| <span data-ttu-id="99255-315">Plain text (text/plain)</span><span class="sxs-lookup"><span data-stu-id="99255-315">Plain text (text/plain)</span></span> |`metadata_content_type`</br>`metadata_content_encoding`</br> | <span data-ttu-id="99255-316">Extract text</span><span class="sxs-lookup"><span data-stu-id="99255-316">Extract text</span></span>|


## <a name="help-us-make-azure-search-better"></a><span data-ttu-id="99255-317">Help us make Azure Search better</span><span class="sxs-lookup"><span data-stu-id="99255-317">Help us make Azure Search better</span></span>
<span data-ttu-id="99255-318">If you have feature requests or ideas for improvements, let us know on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="99255-318">If you have feature requests or ideas for improvements, let us know on our [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).</span></span>
