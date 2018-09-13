---
title: Copy data to/from Azure Blob Storage | Microsoft Docs
description: 'Learn how to copy blob data in Azure Data Factory. Use our sample: How to copy data to and from Azure Blob Storage and Azure SQL Database.'
keywords: blob data, azure blob copy
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: jingwang
ms.openlocfilehash: 16a094b8a311c43658aad299e206d79e29bafed0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672262"
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="7f44c-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7f44c-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="7f44c-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from Azure Blob Storage.</span></span> <span data-ttu-id="7f44c-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="7f44c-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="7f44c-108">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7f44c-108">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="7f44c-109">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="7f44c-109">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f44c-110">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-110">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="7f44c-111">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-111">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="7f44c-112">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span><span class="sxs-lookup"><span data-stu-id="7f44c-112">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
>
> <span data-ttu-id="7f44c-113">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="7f44c-113">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="7f44c-114">If you need to delete source data after a successful copy, create a custom activity to delete the data and use the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7f44c-114">If you need to delete source data after a successful copy, create a custom activity to delete the data and use the activity in the pipeline.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7f44c-115">Getting started</span><span class="sxs-lookup"><span data-stu-id="7f44c-115">Getting started</span></span>
<span data-ttu-id="7f44c-116">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="7f44c-116">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="7f44c-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7f44c-118">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="7f44c-118">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="7f44c-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7f44c-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="7f44c-120">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="7f44c-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="7f44c-121">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="7f44c-122">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7f44c-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7f44c-123">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="7f44c-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="7f44c-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="7f44c-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="7f44c-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="7f44c-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7f44c-126">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="7f44c-126">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7f44c-127">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="7f44c-127">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples) section of this article.</span></span>

<span data-ttu-id="7f44c-128">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="7f44c-128">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7f44c-129">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7f44c-129">Linked service properties</span></span>
<span data-ttu-id="7f44c-130">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7f44c-130">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="7f44c-131">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span><span class="sxs-lookup"><span data-stu-id="7f44c-131">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="7f44c-132">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-132">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="7f44c-133">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-133">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="7f44c-134">There are no other differences between these two linked services.</span><span class="sxs-lookup"><span data-stu-id="7f44c-134">There are no other differences between these two linked services.</span></span> <span data-ttu-id="7f44c-135">Choose the linked service that suits your needs.</span><span class="sxs-lookup"><span data-stu-id="7f44c-135">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="7f44c-136">The following sections provide more details on these two linked services.</span><span class="sxs-lookup"><span data-stu-id="7f44c-136">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="7f44c-137">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7f44c-137">Dataset properties</span></span>
<span data-ttu-id="7f44c-138">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-138">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="7f44c-139">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="7f44c-139">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="7f44c-140">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-140">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="7f44c-141">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="7f44c-141">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7f44c-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="7f44c-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7f44c-143">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="7f44c-143">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="7f44c-144">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="7f44c-144">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="7f44c-145">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="7f44c-145">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="7f44c-146">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span><span class="sxs-lookup"><span data-stu-id="7f44c-146">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="7f44c-147">Property</span><span class="sxs-lookup"><span data-stu-id="7f44c-147">Property</span></span> | <span data-ttu-id="7f44c-148">Description</span><span class="sxs-lookup"><span data-stu-id="7f44c-148">Description</span></span> | <span data-ttu-id="7f44c-149">Required</span><span class="sxs-lookup"><span data-stu-id="7f44c-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f44c-150">folderPath</span><span class="sxs-lookup"><span data-stu-id="7f44c-150">folderPath</span></span> |<span data-ttu-id="7f44c-151">Path to the container and folder in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="7f44c-151">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="7f44c-152">Example: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="7f44c-152">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="7f44c-153">Yes</span><span class="sxs-lookup"><span data-stu-id="7f44c-153">Yes</span></span> |
| <span data-ttu-id="7f44c-154">fileName</span><span class="sxs-lookup"><span data-stu-id="7f44c-154">fileName</span></span> |<span data-ttu-id="7f44c-155">Name of the blob.</span><span class="sxs-lookup"><span data-stu-id="7f44c-155">Name of the blob.</span></span> <span data-ttu-id="7f44c-156">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="7f44c-156">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="7f44c-157">If you specify a filename, the activity (including Copy) works on the specific Blob.</span><span class="sxs-lookup"><span data-stu-id="7f44c-157">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="7f44c-158">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="7f44c-158">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="7f44c-159">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="7f44c-159">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="7f44c-160">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-160">No</span></span> |
| <span data-ttu-id="7f44c-161">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="7f44c-161">partitionedBy</span></span> |<span data-ttu-id="7f44c-162">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="7f44c-162">partitionedBy is an optional property.</span></span> <span data-ttu-id="7f44c-163">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="7f44c-163">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="7f44c-164">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="7f44c-164">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="7f44c-165">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span><span class="sxs-lookup"><span data-stu-id="7f44c-165">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="7f44c-166">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-166">No</span></span> |
| <span data-ttu-id="7f44c-167">format</span><span class="sxs-lookup"><span data-stu-id="7f44c-167">format</span></span> | <span data-ttu-id="7f44c-168">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-168">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7f44c-169">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="7f44c-169">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="7f44c-170">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="7f44c-170">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="7f44c-171">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="7f44c-171">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="7f44c-172">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-172">No</span></span> |
| <span data-ttu-id="7f44c-173">compression</span><span class="sxs-lookup"><span data-stu-id="7f44c-173">compression</span></span> | <span data-ttu-id="7f44c-174">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="7f44c-174">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="7f44c-175">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-175">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="7f44c-176">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-176">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="7f44c-177">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7f44c-177">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="7f44c-178">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-178">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="7f44c-179">Using partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="7f44c-179">Using partitionedBy property</span></span>
<span data-ttu-id="7f44c-180">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="7f44c-180">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="7f44c-181">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span><span class="sxs-lookup"><span data-stu-id="7f44c-181">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="7f44c-182">Sample 1</span><span class="sxs-lookup"><span data-stu-id="7f44c-182">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="7f44c-183">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span><span class="sxs-lookup"><span data-stu-id="7f44c-183">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="7f44c-184">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="7f44c-184">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="7f44c-185">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="7f44c-185">The folderPath is different for each slice.</span></span> <span data-ttu-id="7f44c-186">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="7f44c-186">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="7f44c-187">Sample 2</span><span class="sxs-lookup"><span data-stu-id="7f44c-187">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="7f44c-188">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span><span class="sxs-lookup"><span data-stu-id="7f44c-188">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="7f44c-189">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="7f44c-189">Copy activity properties</span></span>
<span data-ttu-id="7f44c-190">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="7f44c-190">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7f44c-191">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="7f44c-191">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="7f44c-192">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="7f44c-192">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="7f44c-193">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="7f44c-193">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="7f44c-194">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-194">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="7f44c-195">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-195">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="7f44c-196">This section provides a list of properties supported by BlobSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="7f44c-196">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="7f44c-197">**BlobSource** supports the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="7f44c-197">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="7f44c-198">Property</span><span class="sxs-lookup"><span data-stu-id="7f44c-198">Property</span></span> | <span data-ttu-id="7f44c-199">Description</span><span class="sxs-lookup"><span data-stu-id="7f44c-199">Description</span></span> | <span data-ttu-id="7f44c-200">Allowed values</span><span class="sxs-lookup"><span data-stu-id="7f44c-200">Allowed values</span></span> | <span data-ttu-id="7f44c-201">Required</span><span class="sxs-lookup"><span data-stu-id="7f44c-201">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f44c-202">recursive</span><span class="sxs-lookup"><span data-stu-id="7f44c-202">recursive</span></span> |<span data-ttu-id="7f44c-203">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="7f44c-203">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="7f44c-204">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="7f44c-204">True (default value), False</span></span> |<span data-ttu-id="7f44c-205">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-205">No</span></span> |

<span data-ttu-id="7f44c-206">**BlobSink** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="7f44c-206">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="7f44c-207">Property</span><span class="sxs-lookup"><span data-stu-id="7f44c-207">Property</span></span> | <span data-ttu-id="7f44c-208">Description</span><span class="sxs-lookup"><span data-stu-id="7f44c-208">Description</span></span> | <span data-ttu-id="7f44c-209">Allowed values</span><span class="sxs-lookup"><span data-stu-id="7f44c-209">Allowed values</span></span> | <span data-ttu-id="7f44c-210">Required</span><span class="sxs-lookup"><span data-stu-id="7f44c-210">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f44c-211">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="7f44c-211">copyBehavior</span></span> |<span data-ttu-id="7f44c-212">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="7f44c-212">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="7f44c-213"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="7f44c-213"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="7f44c-214">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="7f44c-214">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="7f44c-215"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="7f44c-215"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="7f44c-216">The target files have auto generated name.</span><span class="sxs-lookup"><span data-stu-id="7f44c-216">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="7f44c-217"><b>MergeFiles</b>: merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="7f44c-217"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="7f44c-218">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="7f44c-218">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="7f44c-219">No</span><span class="sxs-lookup"><span data-stu-id="7f44c-219">No</span></span> |

<span data-ttu-id="7f44c-220">**BlobSource** also supports these two properties for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="7f44c-220">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="7f44c-221">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span><span class="sxs-lookup"><span data-stu-id="7f44c-221">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="7f44c-222">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span><span class="sxs-lookup"><span data-stu-id="7f44c-222">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="7f44c-223">It is applicable only when input dataset is using TextFormat.</span><span class="sxs-lookup"><span data-stu-id="7f44c-223">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="7f44c-224">Similarly, **BlobSink** supports the following property for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="7f44c-224">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="7f44c-225">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span><span class="sxs-lookup"><span data-stu-id="7f44c-225">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="7f44c-226">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-226">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="7f44c-227">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span><span class="sxs-lookup"><span data-stu-id="7f44c-227">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="7f44c-228">Copy Activity property</span><span class="sxs-lookup"><span data-stu-id="7f44c-228">Copy Activity property</span></span> | <span data-ttu-id="7f44c-229">Dataset property</span><span class="sxs-lookup"><span data-stu-id="7f44c-229">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f44c-230">skipHeaderLineCount on BlobSource</span><span class="sxs-lookup"><span data-stu-id="7f44c-230">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="7f44c-231">skipLineCount and firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="7f44c-231">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="7f44c-232">Lines are skipped first and then the first row is read as a header.</span><span class="sxs-lookup"><span data-stu-id="7f44c-232">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="7f44c-233">treatEmptyAsNull on BlobSource</span><span class="sxs-lookup"><span data-stu-id="7f44c-233">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="7f44c-234">treatEmptyAsNull on input dataset</span><span class="sxs-lookup"><span data-stu-id="7f44c-234">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="7f44c-235">blobWriterAddHeader on BlobSink</span><span class="sxs-lookup"><span data-stu-id="7f44c-235">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="7f44c-236">firstRowAsHeader on output dataset</span><span class="sxs-lookup"><span data-stu-id="7f44c-236">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="7f44c-237">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span><span class="sxs-lookup"><span data-stu-id="7f44c-237">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="7f44c-238">recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="7f44c-238">recursive and copyBehavior examples</span></span>
<span data-ttu-id="7f44c-239">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span><span class="sxs-lookup"><span data-stu-id="7f44c-239">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="7f44c-240">recursive</span><span class="sxs-lookup"><span data-stu-id="7f44c-240">recursive</span></span> | <span data-ttu-id="7f44c-241">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="7f44c-241">copyBehavior</span></span> | <span data-ttu-id="7f44c-242">Resulting behavior</span><span class="sxs-lookup"><span data-stu-id="7f44c-242">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f44c-243">true</span><span class="sxs-lookup"><span data-stu-id="7f44c-243">true</span></span> |<span data-ttu-id="7f44c-244">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="7f44c-244">preserveHierarchy</span></span> |<span data-ttu-id="7f44c-245">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-245">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-246">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-246">Folder1</span></span><br/><span data-ttu-id="7f44c-247">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-247">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-248">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-248">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-249">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-249">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-250">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-250">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-251">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-251">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-252">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-252">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-253">the target folder Folder1 is created with the same structure as the source</span><span class="sxs-lookup"><span data-stu-id="7f44c-253">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="7f44c-254">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-254">Folder1</span></span><br/><span data-ttu-id="7f44c-255">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-255">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-256">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-256">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-257">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-257">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-258">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-258">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-259">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-259">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-260">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="7f44c-260">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="7f44c-261">true</span><span class="sxs-lookup"><span data-stu-id="7f44c-261">true</span></span> |<span data-ttu-id="7f44c-262">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="7f44c-262">flattenHierarchy</span></span> |<span data-ttu-id="7f44c-263">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-263">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-264">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-264">Folder1</span></span><br/><span data-ttu-id="7f44c-265">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-265">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-266">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-266">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-267">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-267">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-268">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-268">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-271">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-271">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-272">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-272">Folder1</span></span><br/><span data-ttu-id="7f44c-273">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-273">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="7f44c-274">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-274">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="7f44c-275">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-275">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="7f44c-276">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-276">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="7f44c-277">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-277">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="7f44c-278">true</span><span class="sxs-lookup"><span data-stu-id="7f44c-278">true</span></span> |<span data-ttu-id="7f44c-279">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="7f44c-279">mergeFiles</span></span> |<span data-ttu-id="7f44c-280">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-280">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-281">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-281">Folder1</span></span><br/><span data-ttu-id="7f44c-282">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-282">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-283">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-283">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-284">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-284">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-285">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-285">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-288">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-288">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-289">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-289">Folder1</span></span><br/><span data-ttu-id="7f44c-290">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span><span class="sxs-lookup"><span data-stu-id="7f44c-290">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="7f44c-291">false</span><span class="sxs-lookup"><span data-stu-id="7f44c-291">false</span></span> |<span data-ttu-id="7f44c-292">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="7f44c-292">preserveHierarchy</span></span> |<span data-ttu-id="7f44c-293">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-293">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="7f44c-294">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-294">Folder1</span></span><br/><span data-ttu-id="7f44c-295">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-295">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-296">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-296">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-297">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-297">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-298">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-298">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-299">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-299">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-300">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-301">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7f44c-301">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7f44c-302">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-302">Folder1</span></span><br/><span data-ttu-id="7f44c-303">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-303">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-304">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-304">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="7f44c-305">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7f44c-305">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="7f44c-306">false</span><span class="sxs-lookup"><span data-stu-id="7f44c-306">false</span></span> |<span data-ttu-id="7f44c-307">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="7f44c-307">flattenHierarchy</span></span> |<span data-ttu-id="7f44c-308">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-308">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="7f44c-309">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-309">Folder1</span></span><br/><span data-ttu-id="7f44c-310">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-310">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-311">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-311">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-312">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-312">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-313">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-313">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-316">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7f44c-316">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7f44c-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-317">Folder1</span></span><br/><span data-ttu-id="7f44c-318">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-318">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="7f44c-319">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-319">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="7f44c-320">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7f44c-320">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="7f44c-321">false</span><span class="sxs-lookup"><span data-stu-id="7f44c-321">false</span></span> |<span data-ttu-id="7f44c-322">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="7f44c-322">mergeFiles</span></span> |<span data-ttu-id="7f44c-323">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7f44c-323">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="7f44c-324">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-324">Folder1</span></span><br/><span data-ttu-id="7f44c-325">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-325">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="7f44c-326">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="7f44c-326">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="7f44c-327">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-327">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="7f44c-328">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="7f44c-328">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="7f44c-329">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="7f44c-329">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="7f44c-330">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="7f44c-330">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="7f44c-331">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="7f44c-331">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="7f44c-332">Folder1</span><span class="sxs-lookup"><span data-stu-id="7f44c-332">Folder1</span></span><br/><span data-ttu-id="7f44c-333">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="7f44c-333">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="7f44c-334">auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="7f44c-334">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="7f44c-335">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="7f44c-335">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="7f44c-336">Supported file and compression formats</span><span class="sxs-lookup"><span data-stu-id="7f44c-336">Supported file and compression formats</span></span>
<span data-ttu-id="7f44c-337">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span><span class="sxs-lookup"><span data-stu-id="7f44c-337">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="7f44c-338">JSON examples</span><span class="sxs-lookup"><span data-stu-id="7f44c-338">JSON examples</span></span>
<span data-ttu-id="7f44c-339">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7f44c-339">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7f44c-340">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7f44c-340">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="7f44c-341">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7f44c-341">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="7f44c-342">Example: Copy data from Blob Storage to SQL Database</span><span class="sxs-lookup"><span data-stu-id="7f44c-342">Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="7f44c-343">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="7f44c-343">The following sample shows:</span></span>

1. <span data-ttu-id="7f44c-344">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-344">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="7f44c-345">A linked service of type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-345">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="7f44c-346">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-346">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="7f44c-347">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-347">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7f44c-348">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-348">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7f44c-349">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span><span class="sxs-lookup"><span data-stu-id="7f44c-349">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="7f44c-350">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="7f44c-350">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="7f44c-351">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-351">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="7f44c-352">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-352">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="7f44c-353">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-353">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="7f44c-354">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="7f44c-354">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="7f44c-355">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="7f44c-355">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="7f44c-356">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-356">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="7f44c-357">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7f44c-357">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7f44c-358">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="7f44c-358">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7f44c-359">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="7f44c-359">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="7f44c-360">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7f44c-360">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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
<span data-ttu-id="7f44c-361">**Azure SQL output dataset:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-361">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="7f44c-362">The sample copies data to a table named “MyTable” in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="7f44c-362">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="7f44c-363">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="7f44c-363">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="7f44c-364">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="7f44c-364">New rows are added to the table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="7f44c-365">**A copy activity in a pipeline with Blob source and SQL sink:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-365">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="7f44c-366">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="7f44c-366">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7f44c-367">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-367">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
## <a name="example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="7f44c-368">Example: Copy data from Azure SQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="7f44c-368">Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="7f44c-369">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="7f44c-369">The following sample shows:</span></span>

1. <span data-ttu-id="7f44c-370">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-370">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="7f44c-371">A linked service of type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-371">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="7f44c-372">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-372">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="7f44c-373">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-373">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="7f44c-374">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7f44c-374">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="7f44c-375">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="7f44c-375">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="7f44c-376">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="7f44c-376">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="7f44c-377">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-377">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="7f44c-378">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-378">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="7f44c-379">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-379">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="7f44c-380">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="7f44c-380">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="7f44c-381">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="7f44c-381">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="7f44c-382">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-382">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="7f44c-383">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="7f44c-383">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="7f44c-384">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="7f44c-384">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="7f44c-385">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-385">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="7f44c-386">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7f44c-386">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7f44c-387">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="7f44c-387">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7f44c-388">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="7f44c-388">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="7f44c-389">**A copy activity in a pipeline with SQL source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="7f44c-389">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="7f44c-390">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="7f44c-390">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="7f44c-391">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7f44c-391">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="7f44c-392">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="7f44c-392">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
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

> [!NOTE]
> <span data-ttu-id="7f44c-393">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7f44c-393">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7f44c-394">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="7f44c-394">Performance and Tuning</span></span>
<span data-ttu-id="7f44c-395">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="7f44c-395">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
