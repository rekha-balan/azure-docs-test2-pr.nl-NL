---
title: Move data from Amazon Simple Storage Service by using Data Factory | Microsoft Docs
description: Learn about how to move data from Amazon Simple Storage Service (S3) by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: jingwang
ms.openlocfilehash: d153bd715640a637c022c05fb86c45e1322dea14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563274"
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="c0957-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c0957-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="c0957-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="c0957-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="c0957-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="c0957-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c0957-106">You can copy data from Amazon S3 to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="c0957-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="c0957-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="c0957-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c0957-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c0957-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="c0957-109">Required permissions</span><span class="sxs-lookup"><span data-stu-id="c0957-109">Required permissions</span></span>
<span data-ttu-id="c0957-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span><span class="sxs-lookup"><span data-stu-id="c0957-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="c0957-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span><span class="sxs-lookup"><span data-stu-id="c0957-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="c0957-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span><span class="sxs-lookup"><span data-stu-id="c0957-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="c0957-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span><span class="sxs-lookup"><span data-stu-id="c0957-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="c0957-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="c0957-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c0957-115">Getting started</span><span class="sxs-lookup"><span data-stu-id="c0957-115">Getting started</span></span>
<span data-ttu-id="c0957-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span><span class="sxs-lookup"><span data-stu-id="c0957-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="c0957-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="c0957-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c0957-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="c0957-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c0957-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c0957-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="c0957-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="c0957-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c0957-122">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="c0957-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c0957-123">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="c0957-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="c0957-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="c0957-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="c0957-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="c0957-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c0957-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="c0957-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="c0957-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span><span class="sxs-lookup"><span data-stu-id="c0957-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="c0957-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="c0957-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="c0957-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c0957-130">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="c0957-130">Linked service properties</span></span>
<span data-ttu-id="c0957-131">A linked service links a data store to a data factory.</span><span class="sxs-lookup"><span data-stu-id="c0957-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="c0957-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span><span class="sxs-lookup"><span data-stu-id="c0957-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="c0957-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span><span class="sxs-lookup"><span data-stu-id="c0957-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="c0957-134">Property</span><span class="sxs-lookup"><span data-stu-id="c0957-134">Property</span></span> | <span data-ttu-id="c0957-135">Description</span><span class="sxs-lookup"><span data-stu-id="c0957-135">Description</span></span> | <span data-ttu-id="c0957-136">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c0957-136">Allowed values</span></span> | <span data-ttu-id="c0957-137">Required</span><span class="sxs-lookup"><span data-stu-id="c0957-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0957-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="c0957-138">accessKeyID</span></span> |<span data-ttu-id="c0957-139">ID of the secret access key.</span><span class="sxs-lookup"><span data-stu-id="c0957-139">ID of the secret access key.</span></span> |<span data-ttu-id="c0957-140">string</span><span class="sxs-lookup"><span data-stu-id="c0957-140">string</span></span> |<span data-ttu-id="c0957-141">Yes</span><span class="sxs-lookup"><span data-stu-id="c0957-141">Yes</span></span> |
| <span data-ttu-id="c0957-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="c0957-142">secretAccessKey</span></span> |<span data-ttu-id="c0957-143">The secret access key itself.</span><span class="sxs-lookup"><span data-stu-id="c0957-143">The secret access key itself.</span></span> |<span data-ttu-id="c0957-144">Encrypted secret string</span><span class="sxs-lookup"><span data-stu-id="c0957-144">Encrypted secret string</span></span> |<span data-ttu-id="c0957-145">Yes</span><span class="sxs-lookup"><span data-stu-id="c0957-145">Yes</span></span> |

<span data-ttu-id="c0957-146">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="c0957-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c0957-147">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="c0957-147">Dataset properties</span></span>
<span data-ttu-id="c0957-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="c0957-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="c0957-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span><span class="sxs-lookup"><span data-stu-id="c0957-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="c0957-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="c0957-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span><span class="sxs-lookup"><span data-stu-id="c0957-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="c0957-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="c0957-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c0957-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span><span class="sxs-lookup"><span data-stu-id="c0957-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="c0957-154">Property</span><span class="sxs-lookup"><span data-stu-id="c0957-154">Property</span></span> | <span data-ttu-id="c0957-155">Description</span><span class="sxs-lookup"><span data-stu-id="c0957-155">Description</span></span> | <span data-ttu-id="c0957-156">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c0957-156">Allowed values</span></span> | <span data-ttu-id="c0957-157">Required</span><span class="sxs-lookup"><span data-stu-id="c0957-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0957-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="c0957-158">bucketName</span></span> |<span data-ttu-id="c0957-159">The S3 bucket name.</span><span class="sxs-lookup"><span data-stu-id="c0957-159">The S3 bucket name.</span></span> |<span data-ttu-id="c0957-160">String</span><span class="sxs-lookup"><span data-stu-id="c0957-160">String</span></span> |<span data-ttu-id="c0957-161">Yes</span><span class="sxs-lookup"><span data-stu-id="c0957-161">Yes</span></span> |
| <span data-ttu-id="c0957-162">key</span><span class="sxs-lookup"><span data-stu-id="c0957-162">key</span></span> |<span data-ttu-id="c0957-163">The S3 object key.</span><span class="sxs-lookup"><span data-stu-id="c0957-163">The S3 object key.</span></span> |<span data-ttu-id="c0957-164">String</span><span class="sxs-lookup"><span data-stu-id="c0957-164">String</span></span> |<span data-ttu-id="c0957-165">No</span><span class="sxs-lookup"><span data-stu-id="c0957-165">No</span></span> |
| <span data-ttu-id="c0957-166">prefix</span><span class="sxs-lookup"><span data-stu-id="c0957-166">prefix</span></span> |<span data-ttu-id="c0957-167">Prefix for the S3 object key.</span><span class="sxs-lookup"><span data-stu-id="c0957-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="c0957-168">Objects whose keys start with this prefix are selected.</span><span class="sxs-lookup"><span data-stu-id="c0957-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="c0957-169">Applies only when key is empty.</span><span class="sxs-lookup"><span data-stu-id="c0957-169">Applies only when key is empty.</span></span> |<span data-ttu-id="c0957-170">String</span><span class="sxs-lookup"><span data-stu-id="c0957-170">String</span></span> |<span data-ttu-id="c0957-171">No</span><span class="sxs-lookup"><span data-stu-id="c0957-171">No</span></span> |
| <span data-ttu-id="c0957-172">version</span><span class="sxs-lookup"><span data-stu-id="c0957-172">version</span></span> |<span data-ttu-id="c0957-173">The version of the S3 object, if S3 versioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="c0957-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="c0957-174">String</span><span class="sxs-lookup"><span data-stu-id="c0957-174">String</span></span> |<span data-ttu-id="c0957-175">No</span><span class="sxs-lookup"><span data-stu-id="c0957-175">No</span></span> |
| <span data-ttu-id="c0957-176">format</span><span class="sxs-lookup"><span data-stu-id="c0957-176">format</span></span> | <span data-ttu-id="c0957-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c0957-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c0957-178">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="c0957-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c0957-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="c0957-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c0957-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="c0957-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c0957-181">No</span><span class="sxs-lookup"><span data-stu-id="c0957-181">No</span></span> | |
| <span data-ttu-id="c0957-182">compression</span><span class="sxs-lookup"><span data-stu-id="c0957-182">compression</span></span> | <span data-ttu-id="c0957-183">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="c0957-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c0957-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c0957-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c0957-185">The supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="c0957-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c0957-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c0957-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c0957-187">No</span><span class="sxs-lookup"><span data-stu-id="c0957-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="c0957-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span><span class="sxs-lookup"><span data-stu-id="c0957-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="c0957-189">Sample dataset with prefix</span><span class="sxs-lookup"><span data-stu-id="c0957-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="c0957-190">Sample dataset (with version)</span><span class="sxs-lookup"><span data-stu-id="c0957-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="c0957-191">Dynamic paths for S3</span><span class="sxs-lookup"><span data-stu-id="c0957-191">Dynamic paths for S3</span></span>
<span data-ttu-id="c0957-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="c0957-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="c0957-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="c0957-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="c0957-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="c0957-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="c0957-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c0957-196">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="c0957-196">Copy activity properties</span></span>
<span data-ttu-id="c0957-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="c0957-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="c0957-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="c0957-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="c0957-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c0957-200">For the copy activity, properties vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="c0957-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="c0957-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="c0957-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="c0957-202">Property</span><span class="sxs-lookup"><span data-stu-id="c0957-202">Property</span></span> | <span data-ttu-id="c0957-203">Description</span><span class="sxs-lookup"><span data-stu-id="c0957-203">Description</span></span> | <span data-ttu-id="c0957-204">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c0957-204">Allowed values</span></span> | <span data-ttu-id="c0957-205">Required</span><span class="sxs-lookup"><span data-stu-id="c0957-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0957-206">recursive</span><span class="sxs-lookup"><span data-stu-id="c0957-206">recursive</span></span> |<span data-ttu-id="c0957-207">Specifies whether to recursively list S3 objects under the directory.</span><span class="sxs-lookup"><span data-stu-id="c0957-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="c0957-208">true/false</span><span class="sxs-lookup"><span data-stu-id="c0957-208">true/false</span></span> |<span data-ttu-id="c0957-209">No</span><span class="sxs-lookup"><span data-stu-id="c0957-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="c0957-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="c0957-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="c0957-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c0957-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="c0957-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c0957-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="c0957-213">The sample provides JSON definitions for the following Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="c0957-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="c0957-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="c0957-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c0957-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="c0957-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c0957-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c0957-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c0957-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="c0957-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c0957-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c0957-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c0957-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c0957-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="c0957-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="c0957-221">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="c0957-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="c0957-222">Amazon S3 linked service</span><span class="sxs-lookup"><span data-stu-id="c0957-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c0957-223">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="c0957-223">Azure Storage linked service</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="c0957-224">Amazon S3 input dataset</span><span class="sxs-lookup"><span data-stu-id="c0957-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="c0957-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c0957-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="c0957-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c0957-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c0957-227">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="c0957-227">Azure Blob output dataset</span></span>

<span data-ttu-id="c0957-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c0957-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c0957-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="c0957-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c0957-230">The folder path uses the year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="c0957-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="c0957-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span><span class="sxs-lookup"><span data-stu-id="c0957-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="c0957-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="c0957-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="c0957-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c0957-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="c0957-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0957-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0957-235">Next steps</span></span>
<span data-ttu-id="c0957-236">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="c0957-236">See the following articles:</span></span>

* <span data-ttu-id="c0957-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="c0957-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c0957-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>