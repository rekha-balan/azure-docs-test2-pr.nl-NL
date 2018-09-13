---
title: Move data from Amazon Simple Storage Service by using Data Factory | Microsoft Docs
description: Learn about how to move data from Amazon Simple Storage Service (S3) by using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: d895dcdf9eefac01790aab6dc3f36a3feb0a8b12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867545"
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="cd5b5-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cd5b5-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-amazon-simple-storage-service-connector.md)
> * [Version 2 (current version)](../connector-amazon-simple-storage-service.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Amazon S3 connector in V2](../connector-amazon-simple-storage-service.md).

<span data-ttu-id="cd5b5-108">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-108">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="cd5b5-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-109">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="cd5b5-110">You can copy data from Amazon S3 to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-110">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="cd5b5-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-111">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="cd5b5-112">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-112">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="cd5b5-113">Required permissions</span><span class="sxs-lookup"><span data-stu-id="cd5b5-113">Required permissions</span></span>
<span data-ttu-id="cd5b5-114">To copy data from Amazon S3, make sure you have been granted the following permissions:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-114">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="cd5b5-115">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-115">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="cd5b5-116">`s3:ListBucket` for Amazon S3 Bucket Operations.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-116">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="cd5b5-117">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-117">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="cd5b5-118">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-118">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="cd5b5-119">Getting started</span><span class="sxs-lookup"><span data-stu-id="cd5b5-119">Getting started</span></span>
<span data-ttu-id="cd5b5-120">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-120">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="cd5b5-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="cd5b5-122">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-122">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="cd5b5-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cd5b5-124">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-124">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="cd5b5-125">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-125">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="cd5b5-126">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="cd5b5-127">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-127">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="cd5b5-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="cd5b5-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="cd5b5-130">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-130">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="cd5b5-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob-storage) section of this article.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob-storage) section of this article.</span></span>

> [!NOTE]
> For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

<span data-ttu-id="cd5b5-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cd5b5-134">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="cd5b5-134">Linked service properties</span></span>
<span data-ttu-id="cd5b5-135">A linked service links a data store to a data factory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="cd5b5-136">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-136">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="cd5b5-137">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-137">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="cd5b5-138">Property</span><span class="sxs-lookup"><span data-stu-id="cd5b5-138">Property</span></span> | <span data-ttu-id="cd5b5-139">Description</span><span class="sxs-lookup"><span data-stu-id="cd5b5-139">Description</span></span> | <span data-ttu-id="cd5b5-140">Allowed values</span><span class="sxs-lookup"><span data-stu-id="cd5b5-140">Allowed values</span></span> | <span data-ttu-id="cd5b5-141">Required</span><span class="sxs-lookup"><span data-stu-id="cd5b5-141">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5b5-142">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="cd5b5-142">accessKeyID</span></span> |<span data-ttu-id="cd5b5-143">ID of the secret access key.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-143">ID of the secret access key.</span></span> |<span data-ttu-id="cd5b5-144">string</span><span class="sxs-lookup"><span data-stu-id="cd5b5-144">string</span></span> |<span data-ttu-id="cd5b5-145">Yes</span><span class="sxs-lookup"><span data-stu-id="cd5b5-145">Yes</span></span> |
| <span data-ttu-id="cd5b5-146">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="cd5b5-146">secretAccessKey</span></span> |<span data-ttu-id="cd5b5-147">The secret access key itself.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-147">The secret access key itself.</span></span> |<span data-ttu-id="cd5b5-148">Encrypted secret string</span><span class="sxs-lookup"><span data-stu-id="cd5b5-148">Encrypted secret string</span></span> |<span data-ttu-id="cd5b5-149">Yes</span><span class="sxs-lookup"><span data-stu-id="cd5b5-149">Yes</span></span> |

>[!NOTE]
>This connector requires access keys for IAM account to copy data from Amazon S3. [Temporary Security Credential](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html) is not supported.
>

<span data-ttu-id="cd5b5-152">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-152">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="cd5b5-153">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="cd5b5-153">Dataset properties</span></span>
<span data-ttu-id="cd5b5-154">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-154">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="cd5b5-155">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-155">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="cd5b5-156">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-156">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="cd5b5-157">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-157">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="cd5b5-158">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-158">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="cd5b5-159">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-159">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="cd5b5-160">Property</span><span class="sxs-lookup"><span data-stu-id="cd5b5-160">Property</span></span> | <span data-ttu-id="cd5b5-161">Description</span><span class="sxs-lookup"><span data-stu-id="cd5b5-161">Description</span></span> | <span data-ttu-id="cd5b5-162">Allowed values</span><span class="sxs-lookup"><span data-stu-id="cd5b5-162">Allowed values</span></span> | <span data-ttu-id="cd5b5-163">Required</span><span class="sxs-lookup"><span data-stu-id="cd5b5-163">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5b5-164">bucketName</span><span class="sxs-lookup"><span data-stu-id="cd5b5-164">bucketName</span></span> |<span data-ttu-id="cd5b5-165">The S3 bucket name.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-165">The S3 bucket name.</span></span> |<span data-ttu-id="cd5b5-166">String</span><span class="sxs-lookup"><span data-stu-id="cd5b5-166">String</span></span> |<span data-ttu-id="cd5b5-167">Yes</span><span class="sxs-lookup"><span data-stu-id="cd5b5-167">Yes</span></span> |
| <span data-ttu-id="cd5b5-168">key</span><span class="sxs-lookup"><span data-stu-id="cd5b5-168">key</span></span> |<span data-ttu-id="cd5b5-169">The S3 object key.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-169">The S3 object key.</span></span> |<span data-ttu-id="cd5b5-170">String</span><span class="sxs-lookup"><span data-stu-id="cd5b5-170">String</span></span> |<span data-ttu-id="cd5b5-171">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-171">No</span></span> |
| <span data-ttu-id="cd5b5-172">prefix</span><span class="sxs-lookup"><span data-stu-id="cd5b5-172">prefix</span></span> |<span data-ttu-id="cd5b5-173">Prefix for the S3 object key.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-173">Prefix for the S3 object key.</span></span> <span data-ttu-id="cd5b5-174">Objects whose keys start with this prefix are selected.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-174">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="cd5b5-175">Applies only when key is empty.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-175">Applies only when key is empty.</span></span> |<span data-ttu-id="cd5b5-176">String</span><span class="sxs-lookup"><span data-stu-id="cd5b5-176">String</span></span> |<span data-ttu-id="cd5b5-177">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-177">No</span></span> |
| <span data-ttu-id="cd5b5-178">version</span><span class="sxs-lookup"><span data-stu-id="cd5b5-178">version</span></span> |<span data-ttu-id="cd5b5-179">The version of the S3 object, if S3 versioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-179">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="cd5b5-180">String</span><span class="sxs-lookup"><span data-stu-id="cd5b5-180">String</span></span> |<span data-ttu-id="cd5b5-181">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-181">No</span></span> |
| <span data-ttu-id="cd5b5-182">format</span><span class="sxs-lookup"><span data-stu-id="cd5b5-182">format</span></span> | <span data-ttu-id="cd5b5-183">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-183">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cd5b5-184">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-184">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="cd5b5-185">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-185">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cd5b5-186">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-186">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cd5b5-187">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-187">No</span></span> | |
| <span data-ttu-id="cd5b5-188">compression</span><span class="sxs-lookup"><span data-stu-id="cd5b5-188">compression</span></span> | <span data-ttu-id="cd5b5-189">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-189">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="cd5b5-190">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-190">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="cd5b5-191">The supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-191">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cd5b5-192">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-192">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cd5b5-193">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-193">No</span></span> | |


> [!NOTE]
> **bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="cd5b5-195">Sample dataset with prefix</span><span class="sxs-lookup"><span data-stu-id="cd5b5-195">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="cd5b5-196">Sample dataset (with version)</span><span class="sxs-lookup"><span data-stu-id="cd5b5-196">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="cd5b5-197">Dynamic paths for S3</span><span class="sxs-lookup"><span data-stu-id="cd5b5-197">Dynamic paths for S3</span></span>
<span data-ttu-id="cd5b5-198">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-198">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="cd5b5-199">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-199">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="cd5b5-200">You can do the same for the **prefix** property of an Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-200">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="cd5b5-201">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-201">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cd5b5-202">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="cd5b5-202">Copy activity properties</span></span>
<span data-ttu-id="cd5b5-203">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-203">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="cd5b5-204">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-204">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="cd5b5-205">Properties available in the **typeProperties** section of the activity vary with each activity type.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-205">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="cd5b5-206">For the copy activity, properties vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-206">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="cd5b5-207">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-207">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="cd5b5-208">Property</span><span class="sxs-lookup"><span data-stu-id="cd5b5-208">Property</span></span> | <span data-ttu-id="cd5b5-209">Description</span><span class="sxs-lookup"><span data-stu-id="cd5b5-209">Description</span></span> | <span data-ttu-id="cd5b5-210">Allowed values</span><span class="sxs-lookup"><span data-stu-id="cd5b5-210">Allowed values</span></span> | <span data-ttu-id="cd5b5-211">Required</span><span class="sxs-lookup"><span data-stu-id="cd5b5-211">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd5b5-212">recursive</span><span class="sxs-lookup"><span data-stu-id="cd5b5-212">recursive</span></span> |<span data-ttu-id="cd5b5-213">Specifies whether to recursively list S3 objects under the directory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-213">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="cd5b5-214">true/false</span><span class="sxs-lookup"><span data-stu-id="cd5b5-214">true/false</span></span> |<span data-ttu-id="cd5b5-215">No</span><span class="sxs-lookup"><span data-stu-id="cd5b5-215">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="cd5b5-216">JSON example: Copy data from Amazon S3 to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="cd5b5-216">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="cd5b5-217">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-217">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="cd5b5-218">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-218">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="cd5b5-219">The sample provides JSON definitions for the following Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-219">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="cd5b5-220">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-220">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="cd5b5-221">A linked service of type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-221">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="cd5b5-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="cd5b5-223">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-223">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="cd5b5-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="cd5b5-225">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-225">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cd5b5-226">The sample copies data from Amazon S3 to an Azure blob every hour.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-226">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="cd5b5-227">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="cd5b5-228">Amazon S3 linked service</span><span class="sxs-lookup"><span data-stu-id="cd5b5-228">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="cd5b5-229">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="cd5b5-229">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="cd5b5-230">Amazon S3 input dataset</span><span class="sxs-lookup"><span data-stu-id="cd5b5-230">Amazon S3 input dataset</span></span>

<span data-ttu-id="cd5b5-231">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-231">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="cd5b5-232">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-232">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="cd5b5-233">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="cd5b5-233">Azure Blob output dataset</span></span>

<span data-ttu-id="cd5b5-234">Data is written to a new blob every hour (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-234">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cd5b5-235">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-235">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cd5b5-236">The folder path uses the year, month, day, and hours parts of the start time.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-236">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="cd5b5-237">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span><span class="sxs-lookup"><span data-stu-id="cd5b5-237">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="cd5b5-238">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-238">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="cd5b5-239">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cd5b5-239">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a><span data-ttu-id="cd5b5-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd5b5-241">Next steps</span></span>
<span data-ttu-id="cd5b5-242">See the following articles:</span><span class="sxs-lookup"><span data-stu-id="cd5b5-242">See the following articles:</span></span>

* <span data-ttu-id="cd5b5-243">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-243">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="cd5b5-244">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="cd5b5-244">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
