---
title: Push data to Search index by using Data Factory | Microsoft Docs
description: Learn about how to push data to Azure Search Index by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: f68e1077ebc26245b25eae3b0310db74b6d1357e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869147"
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="899ad-103">Push data to an Azure Search index by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="899ad-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-search-connector.md)
> * [Version 2 (current version)](../connector-azure-search.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure Search connector in V2](../connector-azure-search.md).

<span data-ttu-id="899ad-108">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="899ad-108">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="899ad-109">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="899ad-109">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="899ad-110">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span><span class="sxs-lookup"><span data-stu-id="899ad-110">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="899ad-111">Enabling connectivity</span><span class="sxs-lookup"><span data-stu-id="899ad-111">Enabling connectivity</span></span>
<span data-ttu-id="899ad-112">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="899ad-112">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="899ad-113">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span><span class="sxs-lookup"><span data-stu-id="899ad-113">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="899ad-114">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="899ad-114">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="899ad-115">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="899ad-115">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="899ad-116">Getting started</span><span class="sxs-lookup"><span data-stu-id="899ad-116">Getting started</span></span>
<span data-ttu-id="899ad-117">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="899ad-117">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="899ad-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="899ad-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="899ad-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="899ad-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="899ad-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="899ad-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="899ad-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="899ad-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="899ad-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="899ad-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="899ad-123">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="899ad-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="899ad-124">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="899ad-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="899ad-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="899ad-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="899ad-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="899ad-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="899ad-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="899ad-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="899ad-128">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span><span class="sxs-lookup"><span data-stu-id="899ad-128">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="899ad-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span><span class="sxs-lookup"><span data-stu-id="899ad-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="899ad-130">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="899ad-130">Linked service properties</span></span>

<span data-ttu-id="899ad-131">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span><span class="sxs-lookup"><span data-stu-id="899ad-131">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="899ad-132">Property</span><span class="sxs-lookup"><span data-stu-id="899ad-132">Property</span></span> | <span data-ttu-id="899ad-133">Description</span><span class="sxs-lookup"><span data-stu-id="899ad-133">Description</span></span> | <span data-ttu-id="899ad-134">Required</span><span class="sxs-lookup"><span data-stu-id="899ad-134">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="899ad-135">type</span><span class="sxs-lookup"><span data-stu-id="899ad-135">type</span></span> | <span data-ttu-id="899ad-136">The type property must be set to: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="899ad-136">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="899ad-137">Yes</span><span class="sxs-lookup"><span data-stu-id="899ad-137">Yes</span></span> |
| <span data-ttu-id="899ad-138">url</span><span class="sxs-lookup"><span data-stu-id="899ad-138">url</span></span> | <span data-ttu-id="899ad-139">URL for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="899ad-139">URL for the Azure Search service.</span></span> | <span data-ttu-id="899ad-140">Yes</span><span class="sxs-lookup"><span data-stu-id="899ad-140">Yes</span></span> |
| <span data-ttu-id="899ad-141">key</span><span class="sxs-lookup"><span data-stu-id="899ad-141">key</span></span> | <span data-ttu-id="899ad-142">Admin key for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="899ad-142">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="899ad-143">Yes</span><span class="sxs-lookup"><span data-stu-id="899ad-143">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="899ad-144">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="899ad-144">Dataset properties</span></span>

<span data-ttu-id="899ad-145">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="899ad-145">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="899ad-146">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span><span class="sxs-lookup"><span data-stu-id="899ad-146">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="899ad-147">The **typeProperties** section is different for each type of dataset.</span><span class="sxs-lookup"><span data-stu-id="899ad-147">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="899ad-148">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="899ad-148">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="899ad-149">Property</span><span class="sxs-lookup"><span data-stu-id="899ad-149">Property</span></span> | <span data-ttu-id="899ad-150">Description</span><span class="sxs-lookup"><span data-stu-id="899ad-150">Description</span></span> | <span data-ttu-id="899ad-151">Required</span><span class="sxs-lookup"><span data-stu-id="899ad-151">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="899ad-152">type</span><span class="sxs-lookup"><span data-stu-id="899ad-152">type</span></span> | <span data-ttu-id="899ad-153">The type property must be set to **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="899ad-153">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="899ad-154">Yes</span><span class="sxs-lookup"><span data-stu-id="899ad-154">Yes</span></span> |
| <span data-ttu-id="899ad-155">indexName</span><span class="sxs-lookup"><span data-stu-id="899ad-155">indexName</span></span> | <span data-ttu-id="899ad-156">Name of the Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="899ad-156">Name of the Azure Search index.</span></span> <span data-ttu-id="899ad-157">Data Factory does not create the index.</span><span class="sxs-lookup"><span data-stu-id="899ad-157">Data Factory does not create the index.</span></span> <span data-ttu-id="899ad-158">The index must exist in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="899ad-158">The index must exist in Azure Search.</span></span> | <span data-ttu-id="899ad-159">Yes</span><span class="sxs-lookup"><span data-stu-id="899ad-159">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="899ad-160">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="899ad-160">Copy activity properties</span></span>
<span data-ttu-id="899ad-161">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="899ad-161">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="899ad-162">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="899ad-162">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="899ad-163">Whereas, properties available in the typeProperties section vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="899ad-163">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="899ad-164">For Copy Activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="899ad-164">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="899ad-165">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span><span class="sxs-lookup"><span data-stu-id="899ad-165">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="899ad-166">Property</span><span class="sxs-lookup"><span data-stu-id="899ad-166">Property</span></span> | <span data-ttu-id="899ad-167">Description</span><span class="sxs-lookup"><span data-stu-id="899ad-167">Description</span></span> | <span data-ttu-id="899ad-168">Allowed values</span><span class="sxs-lookup"><span data-stu-id="899ad-168">Allowed values</span></span> | <span data-ttu-id="899ad-169">Required</span><span class="sxs-lookup"><span data-stu-id="899ad-169">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="899ad-170">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="899ad-170">WriteBehavior</span></span> | <span data-ttu-id="899ad-171">Specifies whether to merge or replace when a document already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="899ad-171">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="899ad-172">See the [WriteBehavior property](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="899ad-172">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="899ad-173">Merge (default)</span><span class="sxs-lookup"><span data-stu-id="899ad-173">Merge (default)</span></span><br/><span data-ttu-id="899ad-174">Upload</span><span class="sxs-lookup"><span data-stu-id="899ad-174">Upload</span></span>| <span data-ttu-id="899ad-175">No</span><span class="sxs-lookup"><span data-stu-id="899ad-175">No</span></span> |
| <span data-ttu-id="899ad-176">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="899ad-176">WriteBatchSize</span></span> | <span data-ttu-id="899ad-177">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="899ad-177">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="899ad-178">See the [WriteBatchSize property](#writebatchsize-property) for details.</span><span class="sxs-lookup"><span data-stu-id="899ad-178">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="899ad-179">1 to 1,000.</span><span class="sxs-lookup"><span data-stu-id="899ad-179">1 to 1,000.</span></span> <span data-ttu-id="899ad-180">Default value is 1000.</span><span class="sxs-lookup"><span data-stu-id="899ad-180">Default value is 1000.</span></span> | <span data-ttu-id="899ad-181">No</span><span class="sxs-lookup"><span data-stu-id="899ad-181">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="899ad-182">WriteBehavior property</span><span class="sxs-lookup"><span data-stu-id="899ad-182">WriteBehavior property</span></span>
<span data-ttu-id="899ad-183">AzureSearchSink upserts when writing data.</span><span class="sxs-lookup"><span data-stu-id="899ad-183">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="899ad-184">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span><span class="sxs-lookup"><span data-stu-id="899ad-184">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="899ad-185">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="899ad-185">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="899ad-186">**Merge**: combine all the columns in the new document with the existing one.</span><span class="sxs-lookup"><span data-stu-id="899ad-186">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="899ad-187">For columns with null value in the new document, the value in the existing one is preserved.</span><span class="sxs-lookup"><span data-stu-id="899ad-187">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="899ad-188">**Upload**: The new document replaces the existing one.</span><span class="sxs-lookup"><span data-stu-id="899ad-188">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="899ad-189">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span><span class="sxs-lookup"><span data-stu-id="899ad-189">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="899ad-190">The default behavior is **Merge**.</span><span class="sxs-lookup"><span data-stu-id="899ad-190">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="899ad-191">WriteBatchSize Property</span><span class="sxs-lookup"><span data-stu-id="899ad-191">WriteBatchSize Property</span></span>
<span data-ttu-id="899ad-192">Azure Search service supports writing documents as a batch.</span><span class="sxs-lookup"><span data-stu-id="899ad-192">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="899ad-193">A batch can contain 1 to 1,000 Actions.</span><span class="sxs-lookup"><span data-stu-id="899ad-193">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="899ad-194">An action handles one document to perform the upload/merge operation.</span><span class="sxs-lookup"><span data-stu-id="899ad-194">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="899ad-195">Data type support</span><span class="sxs-lookup"><span data-stu-id="899ad-195">Data type support</span></span>
<span data-ttu-id="899ad-196">The following table specifies whether an Azure Search data type is supported or not.</span><span class="sxs-lookup"><span data-stu-id="899ad-196">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="899ad-197">Azure Search data type</span><span class="sxs-lookup"><span data-stu-id="899ad-197">Azure Search data type</span></span> | <span data-ttu-id="899ad-198">Supported in Azure Search Sink</span><span class="sxs-lookup"><span data-stu-id="899ad-198">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="899ad-199">String</span><span class="sxs-lookup"><span data-stu-id="899ad-199">String</span></span> | <span data-ttu-id="899ad-200">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-200">Y</span></span> |
| <span data-ttu-id="899ad-201">Int32</span><span class="sxs-lookup"><span data-stu-id="899ad-201">Int32</span></span> | <span data-ttu-id="899ad-202">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-202">Y</span></span> |
| <span data-ttu-id="899ad-203">Int64</span><span class="sxs-lookup"><span data-stu-id="899ad-203">Int64</span></span> | <span data-ttu-id="899ad-204">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-204">Y</span></span> |
| <span data-ttu-id="899ad-205">Double</span><span class="sxs-lookup"><span data-stu-id="899ad-205">Double</span></span> | <span data-ttu-id="899ad-206">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-206">Y</span></span> |
| <span data-ttu-id="899ad-207">Boolean</span><span class="sxs-lookup"><span data-stu-id="899ad-207">Boolean</span></span> | <span data-ttu-id="899ad-208">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-208">Y</span></span> |
| <span data-ttu-id="899ad-209">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="899ad-209">DataTimeOffset</span></span> | <span data-ttu-id="899ad-210">Y</span><span class="sxs-lookup"><span data-stu-id="899ad-210">Y</span></span> |
| <span data-ttu-id="899ad-211">String Array</span><span class="sxs-lookup"><span data-stu-id="899ad-211">String Array</span></span> | <span data-ttu-id="899ad-212">N</span><span class="sxs-lookup"><span data-stu-id="899ad-212">N</span></span> |
| <span data-ttu-id="899ad-213">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="899ad-213">GeographyPoint</span></span> | <span data-ttu-id="899ad-214">N</span><span class="sxs-lookup"><span data-stu-id="899ad-214">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="899ad-215">JSON example: Copy data from on-premises SQL Server to Azure Search index</span><span class="sxs-lookup"><span data-stu-id="899ad-215">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="899ad-216">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="899ad-216">The following sample shows:</span></span>

1.  <span data-ttu-id="899ad-217">A linked service of type [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="899ad-217">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="899ad-218">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="899ad-218">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="899ad-219">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="899ad-219">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="899ad-220">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="899ad-220">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="899ad-221">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="899ad-221">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="899ad-222">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span><span class="sxs-lookup"><span data-stu-id="899ad-222">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="899ad-223">The JSON properties used in this sample are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="899ad-223">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="899ad-224">As a first step, setup the data management gateway on your on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="899ad-224">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="899ad-225">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span><span class="sxs-lookup"><span data-stu-id="899ad-225">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="899ad-226">**Azure Search linked service:**</span><span class="sxs-lookup"><span data-stu-id="899ad-226">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="899ad-227">**SQL Server linked service**</span><span class="sxs-lookup"><span data-stu-id="899ad-227">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="899ad-228">**SQL Server input dataset**</span><span class="sxs-lookup"><span data-stu-id="899ad-228">**SQL Server input dataset**</span></span>

<span data-ttu-id="899ad-229">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="899ad-229">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="899ad-230">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="899ad-230">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="899ad-231">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="899ad-231">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="899ad-232">**Azure Search output dataset:**</span><span class="sxs-lookup"><span data-stu-id="899ad-232">**Azure Search output dataset:**</span></span>

<span data-ttu-id="899ad-233">The sample copies data to an Azure Search index named **products**.</span><span class="sxs-lookup"><span data-stu-id="899ad-233">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="899ad-234">Data Factory does not create the index.</span><span class="sxs-lookup"><span data-stu-id="899ad-234">Data Factory does not create the index.</span></span> <span data-ttu-id="899ad-235">To test the sample, create an index with this name.</span><span class="sxs-lookup"><span data-stu-id="899ad-235">To test the sample, create an index with this name.</span></span> <span data-ttu-id="899ad-236">Create the Azure Search index with the same number of columns as in the input dataset.</span><span class="sxs-lookup"><span data-stu-id="899ad-236">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="899ad-237">New entries are added to the Azure Search index every hour.</span><span class="sxs-lookup"><span data-stu-id="899ad-237">New entries are added to the Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="899ad-238">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span><span class="sxs-lookup"><span data-stu-id="899ad-238">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="899ad-239">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="899ad-239">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="899ad-240">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="899ad-240">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="899ad-241">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="899ad-241">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

<span data-ttu-id="899ad-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span><span class="sxs-lookup"><span data-stu-id="899ad-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="899ad-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span><span class="sxs-lookup"><span data-stu-id="899ad-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="899ad-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span><span class="sxs-lookup"><span data-stu-id="899ad-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="899ad-245">Copy from a cloud source</span><span class="sxs-lookup"><span data-stu-id="899ad-245">Copy from a cloud source</span></span>
<span data-ttu-id="899ad-246">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span><span class="sxs-lookup"><span data-stu-id="899ad-246">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="899ad-247">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span><span class="sxs-lookup"><span data-stu-id="899ad-247">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="899ad-248">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span><span class="sxs-lookup"><span data-stu-id="899ad-248">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="899ad-249">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span><span class="sxs-lookup"><span data-stu-id="899ad-249">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="899ad-250">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="899ad-250">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="899ad-251">Performance and tuning</span><span class="sxs-lookup"><span data-stu-id="899ad-251">Performance and tuning</span></span>  
<span data-ttu-id="899ad-252">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="899ad-252">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="899ad-253">Next steps</span><span class="sxs-lookup"><span data-stu-id="899ad-253">Next steps</span></span>
<span data-ttu-id="899ad-254">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="899ad-254">See the following articles:</span></span>

* <span data-ttu-id="899ad-255">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="899ad-255">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
