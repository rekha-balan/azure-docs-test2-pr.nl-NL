---
title: Copy data to Search index by using Azure Data Factory | Microsoft Docs
description: Learn about how to push or copy data to an Azure search index by using the Copy Activity in an Azure Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/07/2018
ms.author: jingwang
ms.openlocfilehash: d31859a2af0402789b03447510d510a9658961de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969190"
---
# <a name="copy-data-to-an-azure-search-index-using-azure-data-factory"></a><span data-ttu-id="ca0b4-103">Copy data to an Azure Search index using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ca0b4-103">Copy data to an Azure Search index using Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-azure-search-connector.md)
> * [Current version](connector-azure-search.md)

<span data-ttu-id="ca0b4-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data into Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data into Azure Search index.</span></span> <span data-ttu-id="ca0b4-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="ca0b4-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="ca0b4-108">Supported capabilities</span></span>

<span data-ttu-id="ca0b4-109">You can copy data from any supported source data store into Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-109">You can copy data from any supported source data store into Azure Search index.</span></span> <span data-ttu-id="ca0b4-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ca0b4-111">Getting started</span><span class="sxs-lookup"><span data-stu-id="ca0b4-111">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="ca0b4-112">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Search connector.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-112">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Search connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ca0b4-113">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="ca0b4-113">Linked service properties</span></span>

<span data-ttu-id="ca0b4-114">The following properties are supported for Azure Search linked service:</span><span class="sxs-lookup"><span data-stu-id="ca0b4-114">The following properties are supported for Azure Search linked service:</span></span>

| <span data-ttu-id="ca0b4-115">Property</span><span class="sxs-lookup"><span data-stu-id="ca0b4-115">Property</span></span> | <span data-ttu-id="ca0b4-116">Description</span><span class="sxs-lookup"><span data-stu-id="ca0b4-116">Description</span></span> | <span data-ttu-id="ca0b4-117">Required</span><span class="sxs-lookup"><span data-stu-id="ca0b4-117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca0b4-118">type</span><span class="sxs-lookup"><span data-stu-id="ca0b4-118">type</span></span> | <span data-ttu-id="ca0b4-119">The type property must be set to: **AzureSearch**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-119">The type property must be set to: **AzureSearch**</span></span> | <span data-ttu-id="ca0b4-120">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-120">Yes</span></span> |
| <span data-ttu-id="ca0b4-121">url</span><span class="sxs-lookup"><span data-stu-id="ca0b4-121">url</span></span> | <span data-ttu-id="ca0b4-122">URL for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-122">URL for the Azure Search service.</span></span> | <span data-ttu-id="ca0b4-123">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-123">Yes</span></span> |
| <span data-ttu-id="ca0b4-124">key</span><span class="sxs-lookup"><span data-stu-id="ca0b4-124">key</span></span> | <span data-ttu-id="ca0b4-125">Admin key for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-125">Admin key for the Azure Search service.</span></span> <span data-ttu-id="ca0b4-126">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ca0b4-126">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="ca0b4-127">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-127">Yes</span></span> |
| <span data-ttu-id="ca0b4-128">connectVia</span><span class="sxs-lookup"><span data-stu-id="ca0b4-128">connectVia</span></span> | <span data-ttu-id="ca0b4-129">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-129">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="ca0b4-130">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="ca0b4-130">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="ca0b4-131">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-131">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="ca0b4-132">No</span><span class="sxs-lookup"><span data-stu-id="ca0b4-132">No</span></span> |

> [!IMPORTANT]
> When copying data from a cloud data store into Azure Search index, in Azure Search linked service, you need to refer a Azure Integration Runtime with explicit region in connactVia. Set the region as the one your Azure Search resides. Learn more from [Azure Integration Runtime](concepts-integration-runtime.md#azure-integration-runtime).

<span data-ttu-id="ca0b4-136">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-136">**Example:**</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": {
                "type": "SecureString",
                "value": "<AdminKey>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="ca0b4-137">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="ca0b4-137">Dataset properties</span></span>

<span data-ttu-id="ca0b4-138">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-138">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="ca0b4-139">This section provides a list of properties supported by Azure Search dataset.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-139">This section provides a list of properties supported by Azure Search dataset.</span></span>

<span data-ttu-id="ca0b4-140">To copy data into Azure Search, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-140">To copy data into Azure Search, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="ca0b4-141">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="ca0b4-141">The following properties are supported:</span></span>

| <span data-ttu-id="ca0b4-142">Property</span><span class="sxs-lookup"><span data-stu-id="ca0b4-142">Property</span></span> | <span data-ttu-id="ca0b4-143">Description</span><span class="sxs-lookup"><span data-stu-id="ca0b4-143">Description</span></span> | <span data-ttu-id="ca0b4-144">Required</span><span class="sxs-lookup"><span data-stu-id="ca0b4-144">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca0b4-145">type</span><span class="sxs-lookup"><span data-stu-id="ca0b4-145">type</span></span> | <span data-ttu-id="ca0b4-146">The type property of the dataset must be set to: **AzureSearchIndex**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-146">The type property of the dataset must be set to: **AzureSearchIndex**</span></span> | <span data-ttu-id="ca0b4-147">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-147">Yes</span></span> |
| <span data-ttu-id="ca0b4-148">indexName</span><span class="sxs-lookup"><span data-stu-id="ca0b4-148">indexName</span></span> | <span data-ttu-id="ca0b4-149">Name of the Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-149">Name of the Azure Search index.</span></span> <span data-ttu-id="ca0b4-150">Data Factory does not create the index.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-150">Data Factory does not create the index.</span></span> <span data-ttu-id="ca0b4-151">The index must exist in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-151">The index must exist in Azure Search.</span></span> | <span data-ttu-id="ca0b4-152">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-152">Yes</span></span> |

<span data-ttu-id="ca0b4-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-153">**Example:**</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": {
            "referenceName": "<Azure Search linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties" : {
            "indexName": "products"
        }
   }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="ca0b4-154">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="ca0b4-154">Copy activity properties</span></span>

<span data-ttu-id="ca0b4-155">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-155">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="ca0b4-156">This section provides a list of properties supported by Azure Search source.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-156">This section provides a list of properties supported by Azure Search source.</span></span>

### <a name="azure-search-as-sink"></a><span data-ttu-id="ca0b4-157">Azure Search as sink</span><span class="sxs-lookup"><span data-stu-id="ca0b4-157">Azure Search as sink</span></span>

<span data-ttu-id="ca0b4-158">To copy data into Azure Search, set the source type in the copy activity to **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-158">To copy data into Azure Search, set the source type in the copy activity to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="ca0b4-159">The following properties are supported in the copy activity **sink** section:</span><span class="sxs-lookup"><span data-stu-id="ca0b4-159">The following properties are supported in the copy activity **sink** section:</span></span>

| <span data-ttu-id="ca0b4-160">Property</span><span class="sxs-lookup"><span data-stu-id="ca0b4-160">Property</span></span> | <span data-ttu-id="ca0b4-161">Description</span><span class="sxs-lookup"><span data-stu-id="ca0b4-161">Description</span></span> | <span data-ttu-id="ca0b4-162">Required</span><span class="sxs-lookup"><span data-stu-id="ca0b4-162">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ca0b4-163">type</span><span class="sxs-lookup"><span data-stu-id="ca0b4-163">type</span></span> | <span data-ttu-id="ca0b4-164">The type property of the copy activity source must be set to: **AzureSearchIndexSink**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-164">The type property of the copy activity source must be set to: **AzureSearchIndexSink**</span></span> | <span data-ttu-id="ca0b4-165">Yes</span><span class="sxs-lookup"><span data-stu-id="ca0b4-165">Yes</span></span> |
| <span data-ttu-id="ca0b4-166">writeBehavior</span><span class="sxs-lookup"><span data-stu-id="ca0b4-166">writeBehavior</span></span> | <span data-ttu-id="ca0b4-167">Specifies whether to merge or replace when a document already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="ca0b4-168">See the [WriteBehavior property](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="ca0b4-168">See the [WriteBehavior property](#writebehavior-property).</span></span><br/><br/><span data-ttu-id="ca0b4-169">Allowed values are: **Merge** (default), and **Upload**.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-169">Allowed values are: **Merge** (default), and **Upload**.</span></span> | <span data-ttu-id="ca0b4-170">No</span><span class="sxs-lookup"><span data-stu-id="ca0b4-170">No</span></span> |
| <span data-ttu-id="ca0b4-171">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ca0b4-171">writeBatchSize</span></span> | <span data-ttu-id="ca0b4-172">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-172">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="ca0b4-173">See the [WriteBatchSize property](#writebatchsize-property) for details.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-173">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span><br/><br/><span data-ttu-id="ca0b4-174">Allowed values are: integer 1 to 1,000; default is 1000.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-174">Allowed values are: integer 1 to 1,000; default is 1000.</span></span> | <span data-ttu-id="ca0b4-175">No</span><span class="sxs-lookup"><span data-stu-id="ca0b4-175">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="ca0b4-176">WriteBehavior property</span><span class="sxs-lookup"><span data-stu-id="ca0b4-176">WriteBehavior property</span></span>

<span data-ttu-id="ca0b4-177">AzureSearchSink upserts when writing data.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-177">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="ca0b4-178">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-178">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="ca0b4-179">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="ca0b4-179">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="ca0b4-180">**Merge**: combine all the columns in the new document with the existing one.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-180">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="ca0b4-181">For columns with null value in the new document, the value in the existing one is preserved.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-181">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="ca0b4-182">**Upload**: The new document replaces the existing one.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-182">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="ca0b4-183">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-183">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="ca0b4-184">The default behavior is **Merge**.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-184">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="ca0b4-185">WriteBatchSize Property</span><span class="sxs-lookup"><span data-stu-id="ca0b4-185">WriteBatchSize Property</span></span>

<span data-ttu-id="ca0b4-186">Azure Search service supports writing documents as a batch.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-186">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="ca0b4-187">A batch can contain 1 to 1,000 Actions.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-187">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="ca0b4-188">An action handles one document to perform the upload/merge operation.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-188">An action handles one document to perform the upload/merge operation.</span></span>

<span data-ttu-id="ca0b4-189">**Example:**</span><span class="sxs-lookup"><span data-stu-id="ca0b4-189">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToAzureSearch",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Azure Search output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "AzureSearchIndexSink",
                "writeBehavior": "Merge"
            }
        }
    }
]
```

### <a name="data-type-support"></a><span data-ttu-id="ca0b4-190">Data type support</span><span class="sxs-lookup"><span data-stu-id="ca0b4-190">Data type support</span></span>

<span data-ttu-id="ca0b4-191">The following table specifies whether an Azure Search data type is supported or not.</span><span class="sxs-lookup"><span data-stu-id="ca0b4-191">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="ca0b4-192">Azure Search data type</span><span class="sxs-lookup"><span data-stu-id="ca0b4-192">Azure Search data type</span></span> | <span data-ttu-id="ca0b4-193">Supported in Azure Search Sink</span><span class="sxs-lookup"><span data-stu-id="ca0b4-193">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="ca0b4-194">String</span><span class="sxs-lookup"><span data-stu-id="ca0b4-194">String</span></span> | <span data-ttu-id="ca0b4-195">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-195">Y</span></span> |
| <span data-ttu-id="ca0b4-196">Int32</span><span class="sxs-lookup"><span data-stu-id="ca0b4-196">Int32</span></span> | <span data-ttu-id="ca0b4-197">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-197">Y</span></span> |
| <span data-ttu-id="ca0b4-198">Int64</span><span class="sxs-lookup"><span data-stu-id="ca0b4-198">Int64</span></span> | <span data-ttu-id="ca0b4-199">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-199">Y</span></span> |
| <span data-ttu-id="ca0b4-200">Double</span><span class="sxs-lookup"><span data-stu-id="ca0b4-200">Double</span></span> | <span data-ttu-id="ca0b4-201">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-201">Y</span></span> |
| <span data-ttu-id="ca0b4-202">Boolean</span><span class="sxs-lookup"><span data-stu-id="ca0b4-202">Boolean</span></span> | <span data-ttu-id="ca0b4-203">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-203">Y</span></span> |
| <span data-ttu-id="ca0b4-204">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ca0b4-204">DataTimeOffset</span></span> | <span data-ttu-id="ca0b4-205">Y</span><span class="sxs-lookup"><span data-stu-id="ca0b4-205">Y</span></span> |
| <span data-ttu-id="ca0b4-206">String Array</span><span class="sxs-lookup"><span data-stu-id="ca0b4-206">String Array</span></span> | <span data-ttu-id="ca0b4-207">N</span><span class="sxs-lookup"><span data-stu-id="ca0b4-207">N</span></span> |
| <span data-ttu-id="ca0b4-208">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="ca0b4-208">GeographyPoint</span></span> | <span data-ttu-id="ca0b4-209">N</span><span class="sxs-lookup"><span data-stu-id="ca0b4-209">N</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ca0b4-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="ca0b4-210">Next steps</span></span>
<span data-ttu-id="ca0b4-211">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ca0b4-211">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
