---
title: Copy data to/from Azure Blob Storage | Microsoft Docs
description: 'Learn how to copy blob data in Azure Data Factory. Use our sample: How to copy data to and from Azure Blob Storage and Azure SQL Database.'
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/05/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 2efc20d5a2248fed69f38880a9e75a6ccb2403dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969403"
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="bf828-104">Copy data to or from Azure Blob Storage using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bf828-104">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-blob-connector.md)
> * [Version 2 (current version)](../connector-azure-blob-storage.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure Blob Storage connector in V2](../connector-azure-blob-storage.md).


<span data-ttu-id="bf828-109">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-109">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="bf828-110">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-110">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="bf828-111">Overview</span><span class="sxs-lookup"><span data-stu-id="bf828-111">Overview</span></span>
<span data-ttu-id="bf828-112">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="bf828-112">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="bf828-113">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-113">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="bf828-114">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-114">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="bf828-115">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="bf828-115">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="bf828-116">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="bf828-116">Supported scenarios</span></span>
<span data-ttu-id="bf828-117">You can copy data **from Azure Blob Storage** to the following data stores:</span><span class="sxs-lookup"><span data-stu-id="bf828-117">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="bf828-118">You can copy data from the following data stores **to Azure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="bf828-118">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage. The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**. Azure Premium Storage is not supported as a sink because it is backed by page blobs.
> 
> Copy Activity does not delete data from the source after the data is successfully copied to the destination. If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline. For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a><span data-ttu-id="bf828-125">Get started</span><span class="sxs-lookup"><span data-stu-id="bf828-125">Get started</span></span>
<span data-ttu-id="bf828-126">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="bf828-126">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="bf828-127">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="bf828-127">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="bf828-128">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span><span class="sxs-lookup"><span data-stu-id="bf828-128">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="bf828-129">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="bf828-129">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="bf828-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="bf828-130">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bf828-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-131">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="bf828-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="bf828-132">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="bf828-133">Create a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="bf828-133">Create a **data factory**.</span></span> <span data-ttu-id="bf828-134">A data factory may contain one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="bf828-134">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="bf828-135">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-135">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="bf828-136">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-136">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="bf828-137">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-137">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="bf828-138">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="bf828-138">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="bf828-139">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="bf828-139">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="bf828-140">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-140">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="bf828-141">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-141">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="bf828-142">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="bf828-142">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="bf828-143">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-143">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="bf828-144">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-144">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="bf828-145">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-145">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="bf828-146">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span><span class="sxs-lookup"><span data-stu-id="bf828-146">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="bf828-147">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="bf828-147">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="bf828-148">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="bf828-148">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="bf828-149">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span><span class="sxs-lookup"><span data-stu-id="bf828-149">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="bf828-150">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-150">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bf828-151">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="bf828-151">Linked service properties</span></span>
<span data-ttu-id="bf828-152">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-152">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="bf828-153">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span><span class="sxs-lookup"><span data-stu-id="bf828-153">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="bf828-154">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-154">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="bf828-155">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-155">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="bf828-156">There are no other differences between these two linked services.</span><span class="sxs-lookup"><span data-stu-id="bf828-156">There are no other differences between these two linked services.</span></span> <span data-ttu-id="bf828-157">Choose the linked service that suits your needs.</span><span class="sxs-lookup"><span data-stu-id="bf828-157">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="bf828-158">The following sections provide more details on these two linked services.</span><span class="sxs-lookup"><span data-stu-id="bf828-158">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="bf828-159">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="bf828-159">Dataset properties</span></span>
<span data-ttu-id="bf828-160">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="bf828-160">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="bf828-161">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="bf828-161">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="bf828-162">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-162">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="bf828-163">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="bf828-163">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bf828-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="bf828-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bf828-165">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="bf828-165">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="bf828-166">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="bf828-166">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="bf828-167">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="bf828-167">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="bf828-168">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span><span class="sxs-lookup"><span data-stu-id="bf828-168">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="bf828-169">Property</span><span class="sxs-lookup"><span data-stu-id="bf828-169">Property</span></span> | <span data-ttu-id="bf828-170">Description</span><span class="sxs-lookup"><span data-stu-id="bf828-170">Description</span></span> | <span data-ttu-id="bf828-171">Required</span><span class="sxs-lookup"><span data-stu-id="bf828-171">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf828-172">folderPath</span><span class="sxs-lookup"><span data-stu-id="bf828-172">folderPath</span></span> |<span data-ttu-id="bf828-173">Path to the container and folder in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-173">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="bf828-174">Example: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="bf828-174">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="bf828-175">Yes</span><span class="sxs-lookup"><span data-stu-id="bf828-175">Yes</span></span> |
| <span data-ttu-id="bf828-176">fileName</span><span class="sxs-lookup"><span data-stu-id="bf828-176">fileName</span></span> |<span data-ttu-id="bf828-177">Name of the blob.</span><span class="sxs-lookup"><span data-stu-id="bf828-177">Name of the blob.</span></span> <span data-ttu-id="bf828-178">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="bf828-178">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="bf828-179">If you specify a filename, the activity (including Copy) works on the specific Blob.</span><span class="sxs-lookup"><span data-stu-id="bf828-179">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="bf828-180">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="bf828-180">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="bf828-181">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="bf828-181">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="bf828-182">No</span><span class="sxs-lookup"><span data-stu-id="bf828-182">No</span></span> |
| <span data-ttu-id="bf828-183">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="bf828-183">partitionedBy</span></span> |<span data-ttu-id="bf828-184">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="bf828-184">partitionedBy is an optional property.</span></span> <span data-ttu-id="bf828-185">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="bf828-185">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="bf828-186">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="bf828-186">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="bf828-187">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span><span class="sxs-lookup"><span data-stu-id="bf828-187">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="bf828-188">No</span><span class="sxs-lookup"><span data-stu-id="bf828-188">No</span></span> |
| <span data-ttu-id="bf828-189">format</span><span class="sxs-lookup"><span data-stu-id="bf828-189">format</span></span> | <span data-ttu-id="bf828-190">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="bf828-190">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="bf828-191">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="bf828-191">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="bf828-192">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="bf828-192">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="bf828-193">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="bf828-193">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="bf828-194">No</span><span class="sxs-lookup"><span data-stu-id="bf828-194">No</span></span> |
| <span data-ttu-id="bf828-195">compression</span><span class="sxs-lookup"><span data-stu-id="bf828-195">compression</span></span> | <span data-ttu-id="bf828-196">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="bf828-196">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="bf828-197">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="bf828-197">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="bf828-198">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="bf828-198">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="bf828-199">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="bf828-199">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="bf828-200">No</span><span class="sxs-lookup"><span data-stu-id="bf828-200">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="bf828-201">Using partitionedBy property</span><span class="sxs-lookup"><span data-stu-id="bf828-201">Using partitionedBy property</span></span>
<span data-ttu-id="bf828-202">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="bf828-202">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="bf828-203">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span><span class="sxs-lookup"><span data-stu-id="bf828-203">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="bf828-204">Sample 1</span><span class="sxs-lookup"><span data-stu-id="bf828-204">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="bf828-205">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span><span class="sxs-lookup"><span data-stu-id="bf828-205">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="bf828-206">The SliceStart refers to start time of the slice.</span><span class="sxs-lookup"><span data-stu-id="bf828-206">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="bf828-207">The folderPath is different for each slice.</span><span class="sxs-lookup"><span data-stu-id="bf828-207">The folderPath is different for each slice.</span></span> <span data-ttu-id="bf828-208">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="bf828-208">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="bf828-209">Sample 2</span><span class="sxs-lookup"><span data-stu-id="bf828-209">Sample 2</span></span>

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

<span data-ttu-id="bf828-210">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span><span class="sxs-lookup"><span data-stu-id="bf828-210">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="bf828-211">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="bf828-211">Copy activity properties</span></span>
<span data-ttu-id="bf828-212">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="bf828-212">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bf828-213">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="bf828-213">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="bf828-214">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="bf828-214">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="bf828-215">For Copy activity, they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="bf828-215">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="bf828-216">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="bf828-216">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="bf828-217">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bf828-217">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="bf828-218">This section provides a list of properties supported by BlobSource and BlobSink.</span><span class="sxs-lookup"><span data-stu-id="bf828-218">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="bf828-219">**BlobSource** supports the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="bf828-219">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="bf828-220">Property</span><span class="sxs-lookup"><span data-stu-id="bf828-220">Property</span></span> | <span data-ttu-id="bf828-221">Description</span><span class="sxs-lookup"><span data-stu-id="bf828-221">Description</span></span> | <span data-ttu-id="bf828-222">Allowed values</span><span class="sxs-lookup"><span data-stu-id="bf828-222">Allowed values</span></span> | <span data-ttu-id="bf828-223">Required</span><span class="sxs-lookup"><span data-stu-id="bf828-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf828-224">recursive</span><span class="sxs-lookup"><span data-stu-id="bf828-224">recursive</span></span> |<span data-ttu-id="bf828-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="bf828-226">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="bf828-226">True (default value), False</span></span> |<span data-ttu-id="bf828-227">No</span><span class="sxs-lookup"><span data-stu-id="bf828-227">No</span></span> |

<span data-ttu-id="bf828-228">**BlobSink** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="bf828-228">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="bf828-229">Property</span><span class="sxs-lookup"><span data-stu-id="bf828-229">Property</span></span> | <span data-ttu-id="bf828-230">Description</span><span class="sxs-lookup"><span data-stu-id="bf828-230">Description</span></span> | <span data-ttu-id="bf828-231">Allowed values</span><span class="sxs-lookup"><span data-stu-id="bf828-231">Allowed values</span></span> | <span data-ttu-id="bf828-232">Required</span><span class="sxs-lookup"><span data-stu-id="bf828-232">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf828-233">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="bf828-233">copyBehavior</span></span> |<span data-ttu-id="bf828-234">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="bf828-234">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="bf828-235"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-235"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="bf828-236">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-236">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="bf828-237"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-237"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="bf828-238">The target files have auto generated name.</span><span class="sxs-lookup"><span data-stu-id="bf828-238">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="bf828-239"><b>MergeFiles</b>: merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="bf828-239"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="bf828-240">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="bf828-240">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="bf828-241">No</span><span class="sxs-lookup"><span data-stu-id="bf828-241">No</span></span> |

<span data-ttu-id="bf828-242">**BlobSource** also supports these two properties for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="bf828-242">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="bf828-243">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span><span class="sxs-lookup"><span data-stu-id="bf828-243">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="bf828-244">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span><span class="sxs-lookup"><span data-stu-id="bf828-244">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="bf828-245">It is applicable only when input dataset is using TextFormat.</span><span class="sxs-lookup"><span data-stu-id="bf828-245">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="bf828-246">Similarly, **BlobSink** supports the following property for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="bf828-246">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="bf828-247">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span><span class="sxs-lookup"><span data-stu-id="bf828-247">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="bf828-248">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="bf828-248">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="bf828-249">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span><span class="sxs-lookup"><span data-stu-id="bf828-249">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="bf828-250">Copy Activity property</span><span class="sxs-lookup"><span data-stu-id="bf828-250">Copy Activity property</span></span> | <span data-ttu-id="bf828-251">Dataset property</span><span class="sxs-lookup"><span data-stu-id="bf828-251">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="bf828-252">skipHeaderLineCount on BlobSource</span><span class="sxs-lookup"><span data-stu-id="bf828-252">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="bf828-253">skipLineCount and firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="bf828-253">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="bf828-254">Lines are skipped first and then the first row is read as a header.</span><span class="sxs-lookup"><span data-stu-id="bf828-254">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="bf828-255">treatEmptyAsNull on BlobSource</span><span class="sxs-lookup"><span data-stu-id="bf828-255">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="bf828-256">treatEmptyAsNull on input dataset</span><span class="sxs-lookup"><span data-stu-id="bf828-256">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="bf828-257">blobWriterAddHeader on BlobSink</span><span class="sxs-lookup"><span data-stu-id="bf828-257">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="bf828-258">firstRowAsHeader on output dataset</span><span class="sxs-lookup"><span data-stu-id="bf828-258">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="bf828-259">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span><span class="sxs-lookup"><span data-stu-id="bf828-259">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="bf828-260">recursive and copyBehavior examples</span><span class="sxs-lookup"><span data-stu-id="bf828-260">recursive and copyBehavior examples</span></span>
<span data-ttu-id="bf828-261">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span><span class="sxs-lookup"><span data-stu-id="bf828-261">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="bf828-262">recursive</span><span class="sxs-lookup"><span data-stu-id="bf828-262">recursive</span></span> | <span data-ttu-id="bf828-263">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="bf828-263">copyBehavior</span></span> | <span data-ttu-id="bf828-264">Resulting behavior</span><span class="sxs-lookup"><span data-stu-id="bf828-264">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf828-265">true</span><span class="sxs-lookup"><span data-stu-id="bf828-265">true</span></span> |<span data-ttu-id="bf828-266">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="bf828-266">preserveHierarchy</span></span> |<span data-ttu-id="bf828-267">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-267">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-268">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-268">Folder1</span></span><br/><span data-ttu-id="bf828-269">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-269">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-270">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-270">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-271">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-271">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-272">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-272">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-273">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-273">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-274">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-274">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-275">the target folder Folder1 is created with the same structure as the source</span><span class="sxs-lookup"><span data-stu-id="bf828-275">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="bf828-276">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-276">Folder1</span></span><br/><span data-ttu-id="bf828-277">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-277">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-278">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-278">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-279">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-279">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-280">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-280">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-281">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-281">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-282">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="bf828-282">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="bf828-283">true</span><span class="sxs-lookup"><span data-stu-id="bf828-283">true</span></span> |<span data-ttu-id="bf828-284">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="bf828-284">flattenHierarchy</span></span> |<span data-ttu-id="bf828-285">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-285">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-286">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-286">Folder1</span></span><br/><span data-ttu-id="bf828-287">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-287">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-288">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-288">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-289">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-289">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-290">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-290">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-293">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-293">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-294">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-294">Folder1</span></span><br/><span data-ttu-id="bf828-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="bf828-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="bf828-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="bf828-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="bf828-297">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span><span class="sxs-lookup"><span data-stu-id="bf828-297">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="bf828-298">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span><span class="sxs-lookup"><span data-stu-id="bf828-298">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="bf828-299">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span><span class="sxs-lookup"><span data-stu-id="bf828-299">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="bf828-300">true</span><span class="sxs-lookup"><span data-stu-id="bf828-300">true</span></span> |<span data-ttu-id="bf828-301">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="bf828-301">mergeFiles</span></span> |<span data-ttu-id="bf828-302">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-302">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-303">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-303">Folder1</span></span><br/><span data-ttu-id="bf828-304">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-304">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-305">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-305">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-306">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-306">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-307">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-307">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-308">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-308">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-309">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-309">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-310">the target Folder1 is created with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-310">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-311">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-311">Folder1</span></span><br/><span data-ttu-id="bf828-312">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span><span class="sxs-lookup"><span data-stu-id="bf828-312">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="bf828-313">false</span><span class="sxs-lookup"><span data-stu-id="bf828-313">false</span></span> |<span data-ttu-id="bf828-314">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="bf828-314">preserveHierarchy</span></span> |<span data-ttu-id="bf828-315">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-315">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="bf828-316">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-316">Folder1</span></span><br/><span data-ttu-id="bf828-317">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-317">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-318">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-318">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-319">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-319">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-323">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="bf828-323">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="bf828-324">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-324">Folder1</span></span><br/><span data-ttu-id="bf828-325">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-325">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-326">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-326">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="bf828-327">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="bf828-327">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="bf828-328">false</span><span class="sxs-lookup"><span data-stu-id="bf828-328">false</span></span> |<span data-ttu-id="bf828-329">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="bf828-329">flattenHierarchy</span></span> |<span data-ttu-id="bf828-330">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-330">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="bf828-331">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-331">Folder1</span></span><br/><span data-ttu-id="bf828-332">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-332">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-333">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-333">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-334">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-334">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-338">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="bf828-338">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="bf828-339">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-339">Folder1</span></span><br/><span data-ttu-id="bf828-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="bf828-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="bf828-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span><span class="sxs-lookup"><span data-stu-id="bf828-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="bf828-342">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="bf828-342">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="bf828-343">false</span><span class="sxs-lookup"><span data-stu-id="bf828-343">false</span></span> |<span data-ttu-id="bf828-344">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="bf828-344">mergeFiles</span></span> |<span data-ttu-id="bf828-345">For a source folder Folder1 with the following structure:</span><span class="sxs-lookup"><span data-stu-id="bf828-345">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="bf828-346">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-346">Folder1</span></span><br/><span data-ttu-id="bf828-347">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bf828-347">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bf828-348">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bf828-348">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bf828-349">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="bf828-349">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bf828-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bf828-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bf828-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bf828-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bf828-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bf828-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bf828-353">the target folder Folder1 is created with the following structure</span><span class="sxs-lookup"><span data-stu-id="bf828-353">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="bf828-354">Folder1</span><span class="sxs-lookup"><span data-stu-id="bf828-354">Folder1</span></span><br/><span data-ttu-id="bf828-355">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="bf828-355">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="bf828-356">auto-generated name for File1</span><span class="sxs-lookup"><span data-stu-id="bf828-356">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="bf828-357">Subfolder1 with File3, File4, and File5 are not picked up.</span><span class="sxs-lookup"><span data-stu-id="bf828-357">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="bf828-358">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bf828-358">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="bf828-359">Let's look at how to quickly copy data to/from an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-359">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="bf828-360">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-360">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="bf828-361">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span><span class="sxs-lookup"><span data-stu-id="bf828-361">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="bf828-362">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span><span class="sxs-lookup"><span data-stu-id="bf828-362">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="bf828-363">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf828-363">Prerequisites</span></span>
1. <span data-ttu-id="bf828-364">Create a general-purpose **Azure Storage Account** if you don't have one already.</span><span class="sxs-lookup"><span data-stu-id="bf828-364">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="bf828-365">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="bf828-365">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="bf828-366">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="bf828-366">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
2. <span data-ttu-id="bf828-367">Create a blob container named **adfblobconnector** in the storage account.</span><span class="sxs-lookup"><span data-stu-id="bf828-367">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="bf828-368">Create a folder named **input** in the **adfblobconnector** container.</span><span class="sxs-lookup"><span data-stu-id="bf828-368">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="bf828-369">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="bf828-369">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="bf828-370">Create the data factory</span><span class="sxs-lookup"><span data-stu-id="bf828-370">Create the data factory</span></span>
1. <span data-ttu-id="bf828-371">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf828-371">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bf828-372">Click **Create a resource** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="bf828-372">Click **Create a resource** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="bf828-373">In the **New data factory** pane:</span><span class="sxs-lookup"><span data-stu-id="bf828-373">In the **New data factory** pane:</span></span>   
    1. <span data-ttu-id="bf828-374">Enter **ADFBlobConnectorDF** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="bf828-374">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="bf828-375">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="bf828-375">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="bf828-376">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="bf828-376">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="bf828-377">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="bf828-377">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="bf828-378">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="bf828-378">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="bf828-379">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span><span class="sxs-lookup"><span data-stu-id="bf828-379">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="bf828-380">Select a **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-380">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="bf828-381">Select **Pin to dashboard** check box at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="bf828-381">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="bf828-382">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf828-382">Click **Create**.</span></span>
3. <span data-ttu-id="bf828-383">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-383">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="bf828-384">Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="bf828-384">Copy Wizard</span></span>
1. <span data-ttu-id="bf828-385">On the Data Factory home page, click the **Copy data** tile to launch **Copy Data Wizard** in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="bf828-385">On the Data Factory home page, click the **Copy data** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.
2. <span data-ttu-id="bf828-387">In the **Properties** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-387">In the **Properties** page:</span></span>
    1. <span data-ttu-id="bf828-388">Enter **CopyPipeline** for **Task name**.</span><span class="sxs-lookup"><span data-stu-id="bf828-388">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="bf828-389">The task name is the name of the pipeline in your data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-389">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="bf828-390">Enter a **description** for the task (optional).</span><span class="sxs-lookup"><span data-stu-id="bf828-390">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="bf828-391">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span><span class="sxs-lookup"><span data-stu-id="bf828-391">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="bf828-392">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span><span class="sxs-lookup"><span data-stu-id="bf828-392">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="bf828-393">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span><span class="sxs-lookup"><span data-stu-id="bf828-393">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="bf828-394">Keep the settings for **Recurring pattern**.</span><span class="sxs-lookup"><span data-stu-id="bf828-394">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="bf828-395">This task runs daily between the start and end times you specify in the next step.</span><span class="sxs-lookup"><span data-stu-id="bf828-395">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="bf828-396">Change the **Start date time** to **04/21/2017**.</span><span class="sxs-lookup"><span data-stu-id="bf828-396">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="bf828-397">Change the **End date time** to **04/25/2017**.</span><span class="sxs-lookup"><span data-stu-id="bf828-397">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="bf828-398">You may want to type the date instead of browsing through the calendar.</span><span class="sxs-lookup"><span data-stu-id="bf828-398">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="bf828-399">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-399">Click **Next**.</span></span>
      <span data-ttu-id="bf828-400">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-400">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="bf828-401">On the **Source data store** page, click **Azure Blob Storage** tile.</span><span class="sxs-lookup"><span data-stu-id="bf828-401">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="bf828-402">You use this page to specify the source data store for the copy task.</span><span class="sxs-lookup"><span data-stu-id="bf828-402">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="bf828-403">You can use an existing data store linked service (or) specify a new data store.</span><span class="sxs-lookup"><span data-stu-id="bf828-403">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="bf828-404">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span><span class="sxs-lookup"><span data-stu-id="bf828-404">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="bf828-405">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-405">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="bf828-406">On the **Specify the Azure Blob storage account** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-406">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="bf828-407">Keep the auto-generated name for **Connection name**.</span><span class="sxs-lookup"><span data-stu-id="bf828-407">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="bf828-408">The connection name is the name of the linked service of type: Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-408">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="bf828-409">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span><span class="sxs-lookup"><span data-stu-id="bf828-409">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="bf828-410">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="bf828-410">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="bf828-411">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="bf828-411">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="bf828-412">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span><span class="sxs-lookup"><span data-stu-id="bf828-412">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="bf828-413">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-413">Click **Next**.</span></span> 
      <span data-ttu-id="bf828-414">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-414">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="bf828-415">On **Choose the input file or folder** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-415">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="bf828-416">Double-click **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="bf828-416">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="bf828-417">Select **input**, and click **Choose**.</span><span class="sxs-lookup"><span data-stu-id="bf828-417">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="bf828-418">In this walkthrough, you select the input folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-418">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="bf828-419">You could also select the emp.txt file in the folder instead.</span><span class="sxs-lookup"><span data-stu-id="bf828-419">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="bf828-420">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-420">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="bf828-421">On the **Choose the input file or folder** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-421">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="bf828-422">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span><span class="sxs-lookup"><span data-stu-id="bf828-422">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="bf828-423">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span><span class="sxs-lookup"><span data-stu-id="bf828-423">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="bf828-424">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span><span class="sxs-lookup"><span data-stu-id="bf828-424">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="bf828-425">Do not set **Copy file recursively**.</span><span class="sxs-lookup"><span data-stu-id="bf828-425">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="bf828-426">Select this option to recursively traverse through folders for files to be copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="bf828-426">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="bf828-427">Do not the **binary copy** option.</span><span class="sxs-lookup"><span data-stu-id="bf828-427">Do not the **binary copy** option.</span></span> <span data-ttu-id="bf828-428">Select this option to perform a binary copy of source file to the destination.</span><span class="sxs-lookup"><span data-stu-id="bf828-428">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="bf828-429">Do not select for this walkthrough so that you can see more options in the next pages.</span><span class="sxs-lookup"><span data-stu-id="bf828-429">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="bf828-430">Confirm that the **Compression type** is set to **None**.</span><span class="sxs-lookup"><span data-stu-id="bf828-430">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="bf828-431">Select a value for this option if your source files are compressed in one of the supported formats.</span><span class="sxs-lookup"><span data-stu-id="bf828-431">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="bf828-432">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-432">Click **Next**.</span></span>
    <span data-ttu-id="bf828-433">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-433">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="bf828-434">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span><span class="sxs-lookup"><span data-stu-id="bf828-434">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="bf828-435">Confirm the following options: a.</span><span class="sxs-lookup"><span data-stu-id="bf828-435">Confirm the following options: a.</span></span> <span data-ttu-id="bf828-436">The **file format** is set to **Text format**.</span><span class="sxs-lookup"><span data-stu-id="bf828-436">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="bf828-437">You can see all the supported formats in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bf828-437">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="bf828-438">For example: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="bf828-438">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="bf828-439">b.</span><span class="sxs-lookup"><span data-stu-id="bf828-439">b.</span></span> <span data-ttu-id="bf828-440">The **column delimiter** is set to `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="bf828-440">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="bf828-441">You can see the other column delimiters supported by Data Factory in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bf828-441">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="bf828-442">You can also specify a custom delimiter.</span><span class="sxs-lookup"><span data-stu-id="bf828-442">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="bf828-443">c.</span><span class="sxs-lookup"><span data-stu-id="bf828-443">c.</span></span> <span data-ttu-id="bf828-444">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="bf828-444">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="bf828-445">You can see the other row delimiters supported by Data Factory in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bf828-445">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="bf828-446">You can also specify a custom delimiter.</span><span class="sxs-lookup"><span data-stu-id="bf828-446">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="bf828-447">d.</span><span class="sxs-lookup"><span data-stu-id="bf828-447">d.</span></span> <span data-ttu-id="bf828-448">The **skip line count** is set to **0**.</span><span class="sxs-lookup"><span data-stu-id="bf828-448">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="bf828-449">If you want a few lines to be skipped at the top of the file, enter the number here.</span><span class="sxs-lookup"><span data-stu-id="bf828-449">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="bf828-450">e.</span><span class="sxs-lookup"><span data-stu-id="bf828-450">e.</span></span>  <span data-ttu-id="bf828-451">The **first data row contains column names** is not set.</span><span class="sxs-lookup"><span data-stu-id="bf828-451">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="bf828-452">If the source files contain column names in the first row, select this option.</span><span class="sxs-lookup"><span data-stu-id="bf828-452">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="bf828-453">f.</span><span class="sxs-lookup"><span data-stu-id="bf828-453">f.</span></span> <span data-ttu-id="bf828-454">The **treat empty column value as null** option is set.</span><span class="sxs-lookup"><span data-stu-id="bf828-454">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="bf828-455">Expand **Advanced settings** to see advanced option available.</span><span class="sxs-lookup"><span data-stu-id="bf828-455">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="bf828-456">At the bottom of the page, see the **preview** of data from the emp.txt file.</span><span class="sxs-lookup"><span data-stu-id="bf828-456">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="bf828-457">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span><span class="sxs-lookup"><span data-stu-id="bf828-457">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="bf828-458">Click **Next** after you review the delimiters and preview data.</span><span class="sxs-lookup"><span data-stu-id="bf828-458">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="bf828-459">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-459">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="bf828-460">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-460">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="bf828-461">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="bf828-461">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="bf828-462">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-462">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="bf828-463">On **Specify the Azure Blob storage account** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-463">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="bf828-464">Enter **AzureStorageLinkedService** for the **Connection name** field.</span><span class="sxs-lookup"><span data-stu-id="bf828-464">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="bf828-465">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span><span class="sxs-lookup"><span data-stu-id="bf828-465">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="bf828-466">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="bf828-466">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="bf828-467">Select your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="bf828-467">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="bf828-468">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-468">Click **Next**.</span></span>     
10. <span data-ttu-id="bf828-469">On the **Choose the output file or folder** page:</span><span class="sxs-lookup"><span data-stu-id="bf828-469">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="bf828-470">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span><span class="sxs-lookup"><span data-stu-id="bf828-470">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="bf828-471">Enter **TAB**.</span><span class="sxs-lookup"><span data-stu-id="bf828-471">Enter **TAB**.</span></span>
    7. <span data-ttu-id="bf828-472">For the **year**, select **yyyy**.</span><span class="sxs-lookup"><span data-stu-id="bf828-472">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="bf828-473">For the **month**, confirm that it is set to **MM**.</span><span class="sxs-lookup"><span data-stu-id="bf828-473">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="bf828-474">For the **day**, confirm that it is set to **dd**.</span><span class="sxs-lookup"><span data-stu-id="bf828-474">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="bf828-475">Confirm that the **compression type** is set to **None**.</span><span class="sxs-lookup"><span data-stu-id="bf828-475">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="bf828-476">Confirm that the **copy behavior** is set to **Merge files**.</span><span class="sxs-lookup"><span data-stu-id="bf828-476">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="bf828-477">If the output file with the same name already exists, the new content is added to the same file at the end.</span><span class="sxs-lookup"><span data-stu-id="bf828-477">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="bf828-478">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-478">Click **Next**.</span></span>
    <span data-ttu-id="bf828-479">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-479">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="bf828-480">On the **File format settings** page, review the settings, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-480">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="bf828-481">One of the additional options here is to add a header to the output file.</span><span class="sxs-lookup"><span data-stu-id="bf828-481">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="bf828-482">If you select that option, a header row is added with names of the columns from the schema of the source.</span><span class="sxs-lookup"><span data-stu-id="bf828-482">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="bf828-483">You can rename the default column names when viewing the schema for the source.</span><span class="sxs-lookup"><span data-stu-id="bf828-483">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="bf828-484">For example, you could change the first column to First Name and second column to Last Name.</span><span class="sxs-lookup"><span data-stu-id="bf828-484">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="bf828-485">Then, the output file is generated with a header with these names as column names.</span><span class="sxs-lookup"><span data-stu-id="bf828-485">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="bf828-486">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-486">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="bf828-487">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span><span class="sxs-lookup"><span data-stu-id="bf828-487">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="bf828-488">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="bf828-488">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="bf828-489">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-489">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="bf828-490">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf828-490">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="bf828-491">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-491">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="bf828-492">Review information in the **Summary** page, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bf828-492">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="bf828-493">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span><span class="sxs-lookup"><span data-stu-id="bf828-493">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="bf828-494">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-494">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="bf828-495">Monitor the pipeline (copy task)</span><span class="sxs-lookup"><span data-stu-id="bf828-495">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="bf828-496">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span><span class="sxs-lookup"><span data-stu-id="bf828-496">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="bf828-497">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="bf828-497">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="bf828-498">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="bf828-498">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="bf828-499">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span><span class="sxs-lookup"><span data-stu-id="bf828-499">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="bf828-500">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span><span class="sxs-lookup"><span data-stu-id="bf828-500">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="bf828-501">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span><span class="sxs-lookup"><span data-stu-id="bf828-501">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="bf828-502">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span><span class="sxs-lookup"><span data-stu-id="bf828-502">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="bf828-503">You should see the following folder structure in the output folder:</span><span class="sxs-lookup"><span data-stu-id="bf828-503">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="bf828-504">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span><span class="sxs-lookup"><span data-stu-id="bf828-504">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="bf828-505">Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="bf828-505">Data Factory entities</span></span>
<span data-ttu-id="bf828-506">Now, switch back to the tab with the Data Factory home page.</span><span class="sxs-lookup"><span data-stu-id="bf828-506">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="bf828-507">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span><span class="sxs-lookup"><span data-stu-id="bf828-507">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Data Factory home page with entities](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="bf828-509">Click **Author and deploy** to launch Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="bf828-509">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="bf828-511">You should see the following Data Factory entities in your data factory:</span><span class="sxs-lookup"><span data-stu-id="bf828-511">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="bf828-512">Two linked services.</span><span class="sxs-lookup"><span data-stu-id="bf828-512">Two linked services.</span></span> <span data-ttu-id="bf828-513">One for the source and the other one for the destination.</span><span class="sxs-lookup"><span data-stu-id="bf828-513">One for the source and the other one for the destination.</span></span> <span data-ttu-id="bf828-514">Both the linked services refer to the same Azure Storage account in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="bf828-514">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="bf828-515">Two datasets.</span><span class="sxs-lookup"><span data-stu-id="bf828-515">Two datasets.</span></span> <span data-ttu-id="bf828-516">An input dataset and an output dataset.</span><span class="sxs-lookup"><span data-stu-id="bf828-516">An input dataset and an output dataset.</span></span> <span data-ttu-id="bf828-517">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span><span class="sxs-lookup"><span data-stu-id="bf828-517">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="bf828-518">A pipeline.</span><span class="sxs-lookup"><span data-stu-id="bf828-518">A pipeline.</span></span> <span data-ttu-id="bf828-519">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span><span class="sxs-lookup"><span data-stu-id="bf828-519">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="bf828-520">The following sections provide more information about these entities.</span><span class="sxs-lookup"><span data-stu-id="bf828-520">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="bf828-521">Linked services</span><span class="sxs-lookup"><span data-stu-id="bf828-521">Linked services</span></span>
<span data-ttu-id="bf828-522">You should see two linked services.</span><span class="sxs-lookup"><span data-stu-id="bf828-522">You should see two linked services.</span></span> <span data-ttu-id="bf828-523">One for the source and the other one for the destination.</span><span class="sxs-lookup"><span data-stu-id="bf828-523">One for the source and the other one for the destination.</span></span> <span data-ttu-id="bf828-524">In this walkthrough, both definitions look the same except for the names.</span><span class="sxs-lookup"><span data-stu-id="bf828-524">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="bf828-525">The **type** of the linked service is set to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="bf828-525">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="bf828-526">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span><span class="sxs-lookup"><span data-stu-id="bf828-526">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="bf828-527">Ignore the hubName property in the definition.</span><span class="sxs-lookup"><span data-stu-id="bf828-527">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="bf828-528">Source blob storage linked service</span><span class="sxs-lookup"><span data-stu-id="bf828-528">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="bf828-529">Destination blob storage linked service</span><span class="sxs-lookup"><span data-stu-id="bf828-529">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="bf828-530">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-530">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="bf828-531">Datasets</span><span class="sxs-lookup"><span data-stu-id="bf828-531">Datasets</span></span>
<span data-ttu-id="bf828-532">There are two datasets: an input dataset and an output dataset.</span><span class="sxs-lookup"><span data-stu-id="bf828-532">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="bf828-533">The type of the dataset is set to **AzureBlob** for both.</span><span class="sxs-lookup"><span data-stu-id="bf828-533">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="bf828-534">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span><span class="sxs-lookup"><span data-stu-id="bf828-534">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="bf828-535">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span><span class="sxs-lookup"><span data-stu-id="bf828-535">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="bf828-536">The output dataset points to the **output** folder of the same blob container.</span><span class="sxs-lookup"><span data-stu-id="bf828-536">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="bf828-537">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span><span class="sxs-lookup"><span data-stu-id="bf828-537">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="bf828-538">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="bf828-538">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="bf828-539">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bf828-539">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="bf828-540">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-540">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="bf828-541">Input dataset</span><span class="sxs-lookup"><span data-stu-id="bf828-541">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="bf828-542">Output dataset</span><span class="sxs-lookup"><span data-stu-id="bf828-542">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="bf828-543">Pipeline</span><span class="sxs-lookup"><span data-stu-id="bf828-543">Pipeline</span></span>
<span data-ttu-id="bf828-544">The pipeline has just one activity.</span><span class="sxs-lookup"><span data-stu-id="bf828-544">The pipeline has just one activity.</span></span> <span data-ttu-id="bf828-545">The **type** of the activity is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="bf828-545">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="bf828-546">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span><span class="sxs-lookup"><span data-stu-id="bf828-546">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="bf828-547">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-547">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="bf828-548">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span><span class="sxs-lookup"><span data-stu-id="bf828-548">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="bf828-549">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span><span class="sxs-lookup"><span data-stu-id="bf828-549">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="bf828-550">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span><span class="sxs-lookup"><span data-stu-id="bf828-550">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="bf828-551">JSON examples for copying data to and from Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bf828-551">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="bf828-552">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bf828-552">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bf828-553">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bf828-553">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="bf828-554">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-554">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="bf828-555">JSON Example: Copy data from Blob Storage to SQL Database</span><span class="sxs-lookup"><span data-stu-id="bf828-555">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="bf828-556">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="bf828-556">The following sample shows:</span></span>

1. <span data-ttu-id="bf828-557">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-557">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="bf828-558">A linked service of type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-558">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="bf828-559">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-559">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="bf828-560">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-560">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bf828-561">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-561">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bf828-562">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span><span class="sxs-lookup"><span data-stu-id="bf828-562">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="bf828-563">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="bf828-563">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bf828-564">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="bf828-564">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="bf828-565">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="bf828-565">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="bf828-566">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="bf828-566">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="bf828-567">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="bf828-567">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="bf828-568">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="bf828-568">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="bf828-569">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="bf828-569">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="bf828-570">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="bf828-570">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bf828-571">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="bf828-571">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bf828-572">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span><span class="sxs-lookup"><span data-stu-id="bf828-572">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="bf828-573">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-573">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="bf828-574">**Azure SQL output dataset:**</span><span class="sxs-lookup"><span data-stu-id="bf828-574">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="bf828-575">The sample copies data to a table named “MyTable” in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="bf828-575">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="bf828-576">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span><span class="sxs-lookup"><span data-stu-id="bf828-576">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="bf828-577">New rows are added to the table every hour.</span><span class="sxs-lookup"><span data-stu-id="bf828-577">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="bf828-578">**A copy activity in a pipeline with Blob source and SQL sink:**</span><span class="sxs-lookup"><span data-stu-id="bf828-578">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="bf828-579">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="bf828-579">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bf828-580">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="bf828-580">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="bf828-581">JSON Example: Copy data from Azure SQL to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="bf828-581">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="bf828-582">The following sample shows:</span><span class="sxs-lookup"><span data-stu-id="bf828-582">The following sample shows:</span></span>

1. <span data-ttu-id="bf828-583">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-583">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="bf828-584">A linked service of type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-584">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="bf828-585">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-585">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="bf828-586">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-586">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="bf828-587">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bf828-587">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="bf828-588">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span><span class="sxs-lookup"><span data-stu-id="bf828-588">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="bf828-589">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="bf828-589">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bf828-590">**Azure SQL linked service:**</span><span class="sxs-lookup"><span data-stu-id="bf828-590">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="bf828-591">**Azure Storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="bf828-591">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="bf828-592">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="bf828-592">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="bf828-593">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span><span class="sxs-lookup"><span data-stu-id="bf828-593">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="bf828-594">See [Linked Services](#linked-service-properties) section for details.</span><span class="sxs-lookup"><span data-stu-id="bf828-594">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="bf828-595">**Azure SQL input dataset:**</span><span class="sxs-lookup"><span data-stu-id="bf828-595">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="bf828-596">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span><span class="sxs-lookup"><span data-stu-id="bf828-596">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="bf828-597">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="bf828-597">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="bf828-598">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="bf828-598">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bf828-599">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="bf828-599">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bf828-600">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="bf828-600">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bf828-601">The folder path uses year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="bf828-601">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="bf828-602">**A copy activity in a pipeline with SQL source and Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="bf828-602">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="bf828-603">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="bf828-603">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bf828-604">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bf828-604">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="bf828-605">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span><span class="sxs-lookup"><span data-stu-id="bf828-605">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a><span data-ttu-id="bf828-607">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="bf828-607">Performance and Tuning</span></span>
<span data-ttu-id="bf828-608">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="bf828-608">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
