---
title: Copy data from Amazon Simple Storage Service using Azure Data Factory | Microsoft Docs
description: Learn about how to copy data from Amazon Simple Storage Service (S3) to supported sink data stores by using Azure Data Factory.
services: data-factory
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 05/25/2018
ms.author: jingwang
ms.openlocfilehash: 3635e8bf1d9ba4061da5b8f416a3b755f7064000
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855886"
---
# <a name="copy-data-from-amazon-simple-storage-service-using-azure-data-factory"></a><span data-ttu-id="299c7-103">Copy data from Amazon Simple Storage Service using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="299c7-103">Copy data from Amazon Simple Storage Service using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-amazon-simple-storage-service-connector.md)
> * [Current version](connector-amazon-simple-storage-service.md)

<span data-ttu-id="299c7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="299c7-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Amazon S3.</span></span> <span data-ttu-id="299c7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="299c7-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="299c7-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="299c7-108">Supported capabilities</span></span>

<span data-ttu-id="299c7-109">You can copy data Amazon S3 to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="299c7-109">You can copy data Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="299c7-110">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="299c7-110">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="299c7-111">Specifically, this Amazon S3 connector supports copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="299c7-111">Specifically, this Amazon S3 connector supports copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="299c7-112">Required permissions</span><span class="sxs-lookup"><span data-stu-id="299c7-112">Required permissions</span></span>

<span data-ttu-id="299c7-113">To copy data from Amazon S3, make sure you have been granted the following permissions:</span><span class="sxs-lookup"><span data-stu-id="299c7-113">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

- <span data-ttu-id="299c7-114">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span><span class="sxs-lookup"><span data-stu-id="299c7-114">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
- <span data-ttu-id="299c7-115">`s3:ListBucket` or `s3:GetBucketLocation` for Amazon S3 Bucket Operations.</span><span class="sxs-lookup"><span data-stu-id="299c7-115">`s3:ListBucket` or `s3:GetBucketLocation` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="299c7-116">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span><span class="sxs-lookup"><span data-stu-id="299c7-116">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="299c7-117">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="299c7-117">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="299c7-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="299c7-118">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)] 

<span data-ttu-id="299c7-119">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="299c7-119">The following sections provide details about properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="299c7-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="299c7-120">Linked service properties</span></span>

<span data-ttu-id="299c7-121">The following properties are supported for Amazon S3 linked service:</span><span class="sxs-lookup"><span data-stu-id="299c7-121">The following properties are supported for Amazon S3 linked service:</span></span>

| <span data-ttu-id="299c7-122">Property</span><span class="sxs-lookup"><span data-stu-id="299c7-122">Property</span></span> | <span data-ttu-id="299c7-123">Description</span><span class="sxs-lookup"><span data-stu-id="299c7-123">Description</span></span> | <span data-ttu-id="299c7-124">Required</span><span class="sxs-lookup"><span data-stu-id="299c7-124">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="299c7-125">type</span><span class="sxs-lookup"><span data-stu-id="299c7-125">type</span></span> | <span data-ttu-id="299c7-126">The type property must be set to **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="299c7-126">The type property must be set to **AmazonS3**.</span></span> | <span data-ttu-id="299c7-127">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-127">Yes</span></span> |
| <span data-ttu-id="299c7-128">accessKeyId</span><span class="sxs-lookup"><span data-stu-id="299c7-128">accessKeyId</span></span> | <span data-ttu-id="299c7-129">ID of the secret access key.</span><span class="sxs-lookup"><span data-stu-id="299c7-129">ID of the secret access key.</span></span> |<span data-ttu-id="299c7-130">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-130">Yes</span></span> |
| <span data-ttu-id="299c7-131">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="299c7-131">secretAccessKey</span></span> | <span data-ttu-id="299c7-132">The secret access key itself.</span><span class="sxs-lookup"><span data-stu-id="299c7-132">The secret access key itself.</span></span> <span data-ttu-id="299c7-133">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="299c7-133">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="299c7-134">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-134">Yes</span></span> |
| <span data-ttu-id="299c7-135">connectVia</span><span class="sxs-lookup"><span data-stu-id="299c7-135">connectVia</span></span> | <span data-ttu-id="299c7-136">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="299c7-136">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="299c7-137">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="299c7-137">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="299c7-138">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="299c7-138">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="299c7-139">No</span><span class="sxs-lookup"><span data-stu-id="299c7-139">No</span></span> |

>[!NOTE]
>This connector requires access keys for IAM account to copy data from Amazon S3. [Temporary Security Credential](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html) is not supported.
>

<span data-ttu-id="299c7-142">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="299c7-142">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AmazonS3",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": {
                    "type": "SecureString",
                    "value": "<secret access key>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="299c7-143">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="299c7-143">Dataset properties</span></span>

<span data-ttu-id="299c7-144">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="299c7-144">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="299c7-145">This section provides a list of properties supported by Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="299c7-145">This section provides a list of properties supported by Amazon S3 dataset.</span></span>

<span data-ttu-id="299c7-146">To copy data from Amazon S3, set the type property of the dataset to **AmazonS3Object**.</span><span class="sxs-lookup"><span data-stu-id="299c7-146">To copy data from Amazon S3, set the type property of the dataset to **AmazonS3Object**.</span></span> <span data-ttu-id="299c7-147">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="299c7-147">The following properties are supported:</span></span>

| <span data-ttu-id="299c7-148">Property</span><span class="sxs-lookup"><span data-stu-id="299c7-148">Property</span></span> | <span data-ttu-id="299c7-149">Description</span><span class="sxs-lookup"><span data-stu-id="299c7-149">Description</span></span> | <span data-ttu-id="299c7-150">Required</span><span class="sxs-lookup"><span data-stu-id="299c7-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="299c7-151">type</span><span class="sxs-lookup"><span data-stu-id="299c7-151">type</span></span> | <span data-ttu-id="299c7-152">The type property of the dataset must be set to: **AmazonS3Object**</span><span class="sxs-lookup"><span data-stu-id="299c7-152">The type property of the dataset must be set to: **AmazonS3Object**</span></span> |<span data-ttu-id="299c7-153">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-153">Yes</span></span> |
| <span data-ttu-id="299c7-154">bucketName</span><span class="sxs-lookup"><span data-stu-id="299c7-154">bucketName</span></span> | <span data-ttu-id="299c7-155">The S3 bucket name.</span><span class="sxs-lookup"><span data-stu-id="299c7-155">The S3 bucket name.</span></span> <span data-ttu-id="299c7-156">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="299c7-156">Wildcard filter is not supported.</span></span> |<span data-ttu-id="299c7-157">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-157">Yes</span></span> |
| <span data-ttu-id="299c7-158">key</span><span class="sxs-lookup"><span data-stu-id="299c7-158">key</span></span> | <span data-ttu-id="299c7-159">The **name or wildcard filter** of S3 object key under the specified bucket.</span><span class="sxs-lookup"><span data-stu-id="299c7-159">The **name or wildcard filter** of S3 object key under the specified bucket.</span></span> <span data-ttu-id="299c7-160">Applies only when "prefix" property is not specified.</span><span class="sxs-lookup"><span data-stu-id="299c7-160">Applies only when "prefix" property is not specified.</span></span> <br/><br/><span data-ttu-id="299c7-161">The wildcard filter is only supported for file name part but not folder part.</span><span class="sxs-lookup"><span data-stu-id="299c7-161">The wildcard filter is only supported for file name part but not folder part.</span></span> <span data-ttu-id="299c7-162">Allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span><span class="sxs-lookup"><span data-stu-id="299c7-162">Allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span></span><br/><span data-ttu-id="299c7-163">- Example 1: `"key": "rootfolder/subfolder/*.csv"`</span><span class="sxs-lookup"><span data-stu-id="299c7-163">- Example 1: `"key": "rootfolder/subfolder/*.csv"`</span></span><br/><span data-ttu-id="299c7-164">- Example 2: `"key": "rootfolder/subfolder/???20180427.txt"`</span><span class="sxs-lookup"><span data-stu-id="299c7-164">- Example 2: `"key": "rootfolder/subfolder/???20180427.txt"`</span></span><br/><span data-ttu-id="299c7-165">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span><span class="sxs-lookup"><span data-stu-id="299c7-165">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span></span> |<span data-ttu-id="299c7-166">No</span><span class="sxs-lookup"><span data-stu-id="299c7-166">No</span></span> |
| <span data-ttu-id="299c7-167">prefix</span><span class="sxs-lookup"><span data-stu-id="299c7-167">prefix</span></span> | <span data-ttu-id="299c7-168">Prefix for the S3 object key.</span><span class="sxs-lookup"><span data-stu-id="299c7-168">Prefix for the S3 object key.</span></span> <span data-ttu-id="299c7-169">Objects whose keys start with this prefix are selected.</span><span class="sxs-lookup"><span data-stu-id="299c7-169">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="299c7-170">Applies only when "key" property is not specified.</span><span class="sxs-lookup"><span data-stu-id="299c7-170">Applies only when "key" property is not specified.</span></span> |<span data-ttu-id="299c7-171">No</span><span class="sxs-lookup"><span data-stu-id="299c7-171">No</span></span> |
| <span data-ttu-id="299c7-172">version</span><span class="sxs-lookup"><span data-stu-id="299c7-172">version</span></span> | <span data-ttu-id="299c7-173">The version of the S3 object, if S3 versioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="299c7-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="299c7-174">No</span><span class="sxs-lookup"><span data-stu-id="299c7-174">No</span></span> |
| <span data-ttu-id="299c7-175">format</span><span class="sxs-lookup"><span data-stu-id="299c7-175">format</span></span> | <span data-ttu-id="299c7-176">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="299c7-176">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="299c7-177">If you want to parse or generate files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="299c7-177">If you want to parse or generate files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="299c7-178">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="299c7-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="299c7-179">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="299c7-179">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="299c7-180">No (only for binary copy scenario)</span><span class="sxs-lookup"><span data-stu-id="299c7-180">No (only for binary copy scenario)</span></span> |
| <span data-ttu-id="299c7-181">compression</span><span class="sxs-lookup"><span data-stu-id="299c7-181">compression</span></span> | <span data-ttu-id="299c7-182">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="299c7-182">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="299c7-183">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="299c7-183">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="299c7-184">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="299c7-184">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="299c7-185">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="299c7-185">Supported levels are: **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="299c7-186">No</span><span class="sxs-lookup"><span data-stu-id="299c7-186">No</span></span> |

>[!TIP]
>To copy all files under a folder, specify **bucketName** for bucket and **prefix** for folder part.<br>To copy a single file with a given name, specify **bucketName** for bucket and **key** for folder part plus file name.<br>To copy a subset of files under a folder, specify **bucketName** for bucket and **key** for folder part plus wildcard filter.

<span data-ttu-id="299c7-190">**Example: using prefix**</span><span class="sxs-lookup"><span data-stu-id="299c7-190">**Example: using prefix**</span></span>

```json
{
    "name": "AmazonS3Dataset",
    "properties": {
        "type": "AmazonS3Object",
        "linkedServiceName": {
            "referenceName": "<Amazon S3 linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "bucketName": "testbucket",
            "prefix": "testFolder/test",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

<span data-ttu-id="299c7-191">**Example: using key and version (optional)**</span><span class="sxs-lookup"><span data-stu-id="299c7-191">**Example: using key and version (optional)**</span></span>

```json
{
    "name": "AmazonS3Dataset",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": {
            "referenceName": "<Amazon S3 linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "bucketName": "testbucket",
            "key": "testFolder/testfile.csv.gz",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="299c7-192">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="299c7-192">Copy activity properties</span></span>

<span data-ttu-id="299c7-193">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="299c7-193">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="299c7-194">This section provides a list of properties supported by Amazon S3 source.</span><span class="sxs-lookup"><span data-stu-id="299c7-194">This section provides a list of properties supported by Amazon S3 source.</span></span>

### <a name="amazon-s3-as-source"></a><span data-ttu-id="299c7-195">Amazon S3 as source</span><span class="sxs-lookup"><span data-stu-id="299c7-195">Amazon S3 as source</span></span>

<span data-ttu-id="299c7-196">To copy data from Amazon S3, set the source type in the copy activity to **FileSystemSource** (which includes Amazon S3).</span><span class="sxs-lookup"><span data-stu-id="299c7-196">To copy data from Amazon S3, set the source type in the copy activity to **FileSystemSource** (which includes Amazon S3).</span></span> <span data-ttu-id="299c7-197">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="299c7-197">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="299c7-198">Property</span><span class="sxs-lookup"><span data-stu-id="299c7-198">Property</span></span> | <span data-ttu-id="299c7-199">Description</span><span class="sxs-lookup"><span data-stu-id="299c7-199">Description</span></span> | <span data-ttu-id="299c7-200">Required</span><span class="sxs-lookup"><span data-stu-id="299c7-200">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="299c7-201">type</span><span class="sxs-lookup"><span data-stu-id="299c7-201">type</span></span> | <span data-ttu-id="299c7-202">The type property of the copy activity source must be set to: **FileSystemSource**</span><span class="sxs-lookup"><span data-stu-id="299c7-202">The type property of the copy activity source must be set to: **FileSystemSource**</span></span> |<span data-ttu-id="299c7-203">Yes</span><span class="sxs-lookup"><span data-stu-id="299c7-203">Yes</span></span> |
| <span data-ttu-id="299c7-204">recursive</span><span class="sxs-lookup"><span data-stu-id="299c7-204">recursive</span></span> | <span data-ttu-id="299c7-205">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="299c7-205">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> <span data-ttu-id="299c7-206">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span><span class="sxs-lookup"><span data-stu-id="299c7-206">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span></span><br/><span data-ttu-id="299c7-207">Allowed values are: **true** (default), **false**</span><span class="sxs-lookup"><span data-stu-id="299c7-207">Allowed values are: **true** (default), **false**</span></span> | <span data-ttu-id="299c7-208">No</span><span class="sxs-lookup"><span data-stu-id="299c7-208">No</span></span> |

<span data-ttu-id="299c7-209">**Example:**</span><span class="sxs-lookup"><span data-stu-id="299c7-209">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromAmazonS3",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Amazon S3 input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "FileSystemSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```
## <a name="next-steps"></a><span data-ttu-id="299c7-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="299c7-210">Next steps</span></span>
<span data-ttu-id="299c7-211">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="299c7-211">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
