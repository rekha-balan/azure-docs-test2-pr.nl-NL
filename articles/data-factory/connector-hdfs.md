---
title: Copy data from HDFS using Azure Data Factory  | Microsoft Docs
description: Learn how to copy data from a cloud or on-premises HDFS source to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 04/27/2018
ms.author: jingwang
ms.openlocfilehash: 034c9a321f402bada87290f6aa72fc7e416ef2c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871424"
---
# <a name="copy-data-from-hdfs-using-azure-data-factory"></a><span data-ttu-id="c1277-103">Copy data from HDFS using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c1277-103">Copy data from HDFS using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-hdfs-connector.md)
> * [Current version](connector-hdfs.md)

<span data-ttu-id="c1277-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from HDFS.</span><span class="sxs-lookup"><span data-stu-id="c1277-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from HDFS.</span></span> <span data-ttu-id="c1277-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="c1277-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="c1277-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="c1277-108">Supported capabilities</span></span>

<span data-ttu-id="c1277-109">You can copy data from HDFS to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="c1277-109">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="c1277-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="c1277-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="c1277-111">Specifically, this HDFS connector supports:</span><span class="sxs-lookup"><span data-stu-id="c1277-111">Specifically, this HDFS connector supports:</span></span>

- <span data-ttu-id="c1277-112">Copying files using **Windows** (Kerberos) or **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="c1277-112">Copying files using **Windows** (Kerberos) or **Anonymous** authentication.</span></span>
- <span data-ttu-id="c1277-113">Copying files using **webhdfs** protocol or **built-in DistCp** support.</span><span class="sxs-lookup"><span data-stu-id="c1277-113">Copying files using **webhdfs** protocol or **built-in DistCp** support.</span></span>
- <span data-ttu-id="c1277-114">Copying files as-is or parsing/generating files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="c1277-114">Copying files as-is or parsing/generating files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1277-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c1277-115">Prerequisites</span></span>

<span data-ttu-id="c1277-116">To copy data from an HDFS that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="c1277-116">To copy data from an HDFS that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="c1277-117">See [Self-hosted Integration Runtime](concepts-integration-runtime.md) article to learn details.</span><span class="sxs-lookup"><span data-stu-id="c1277-117">See [Self-hosted Integration Runtime](concepts-integration-runtime.md) article to learn details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c1277-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="c1277-118">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="c1277-119">The following sections provide details about properties that are used to define Data Factory entities specific to HDFS.</span><span class="sxs-lookup"><span data-stu-id="c1277-119">The following sections provide details about properties that are used to define Data Factory entities specific to HDFS.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c1277-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="c1277-120">Linked service properties</span></span>

<span data-ttu-id="c1277-121">The following properties are supported for HDFS linked service:</span><span class="sxs-lookup"><span data-stu-id="c1277-121">The following properties are supported for HDFS linked service:</span></span>

| <span data-ttu-id="c1277-122">Property</span><span class="sxs-lookup"><span data-stu-id="c1277-122">Property</span></span> | <span data-ttu-id="c1277-123">Description</span><span class="sxs-lookup"><span data-stu-id="c1277-123">Description</span></span> | <span data-ttu-id="c1277-124">Required</span><span class="sxs-lookup"><span data-stu-id="c1277-124">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c1277-125">type</span><span class="sxs-lookup"><span data-stu-id="c1277-125">type</span></span> | <span data-ttu-id="c1277-126">The type property must be set to: **Hdfs**.</span><span class="sxs-lookup"><span data-stu-id="c1277-126">The type property must be set to: **Hdfs**.</span></span> | <span data-ttu-id="c1277-127">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-127">Yes</span></span> |
| <span data-ttu-id="c1277-128">url</span><span class="sxs-lookup"><span data-stu-id="c1277-128">url</span></span> |<span data-ttu-id="c1277-129">URL to the HDFS</span><span class="sxs-lookup"><span data-stu-id="c1277-129">URL to the HDFS</span></span> |<span data-ttu-id="c1277-130">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-130">Yes</span></span> |
| <span data-ttu-id="c1277-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c1277-131">authenticationType</span></span> | <span data-ttu-id="c1277-132">Allowed values are: **Anonymous**, or **Windows**.</span><span class="sxs-lookup"><span data-stu-id="c1277-132">Allowed values are: **Anonymous**, or **Windows**.</span></span> <br><br> <span data-ttu-id="c1277-133">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span><span class="sxs-lookup"><span data-stu-id="c1277-133">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="c1277-134">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-134">Yes</span></span> |
| <span data-ttu-id="c1277-135">userName</span><span class="sxs-lookup"><span data-stu-id="c1277-135">userName</span></span> |<span data-ttu-id="c1277-136">Username for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="c1277-136">Username for Windows authentication.</span></span> <span data-ttu-id="c1277-137">For Kerberos authentication, specify `<username>@<domain>.com`.</span><span class="sxs-lookup"><span data-stu-id="c1277-137">For Kerberos authentication, specify `<username>@<domain>.com`.</span></span> |<span data-ttu-id="c1277-138">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="c1277-138">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="c1277-139">password</span><span class="sxs-lookup"><span data-stu-id="c1277-139">password</span></span> |<span data-ttu-id="c1277-140">Password for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="c1277-140">Password for Windows authentication.</span></span> <span data-ttu-id="c1277-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c1277-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="c1277-142">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="c1277-142">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="c1277-143">connectVia</span><span class="sxs-lookup"><span data-stu-id="c1277-143">connectVia</span></span> | <span data-ttu-id="c1277-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="c1277-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="c1277-145">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="c1277-145">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="c1277-146">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="c1277-146">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="c1277-147">No</span><span class="sxs-lookup"><span data-stu-id="c1277-147">No</span></span> |

<span data-ttu-id="c1277-148">**Example: using Anonymous authentication**</span><span class="sxs-lookup"><span data-stu-id="c1277-148">**Example: using Anonymous authentication**</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "authenticationType": "Anonymous",
            "userName": "hadoop"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="c1277-149">**Example: using Windows authentication**</span><span class="sxs-lookup"><span data-stu-id="c1277-149">**Example: using Windows authentication**</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "authenticationType": "Windows",
            "userName": "<username>@<domain>.com (for Kerberos auth)",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c1277-150">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="c1277-150">Dataset properties</span></span>

<span data-ttu-id="c1277-151">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="c1277-151">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="c1277-152">This section provides a list of properties supported by HDFS dataset.</span><span class="sxs-lookup"><span data-stu-id="c1277-152">This section provides a list of properties supported by HDFS dataset.</span></span>

<span data-ttu-id="c1277-153">To copy data from HDFS, set the type property of the dataset to **FileShare**.</span><span class="sxs-lookup"><span data-stu-id="c1277-153">To copy data from HDFS, set the type property of the dataset to **FileShare**.</span></span> <span data-ttu-id="c1277-154">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="c1277-154">The following properties are supported:</span></span>

| <span data-ttu-id="c1277-155">Property</span><span class="sxs-lookup"><span data-stu-id="c1277-155">Property</span></span> | <span data-ttu-id="c1277-156">Description</span><span class="sxs-lookup"><span data-stu-id="c1277-156">Description</span></span> | <span data-ttu-id="c1277-157">Required</span><span class="sxs-lookup"><span data-stu-id="c1277-157">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c1277-158">type</span><span class="sxs-lookup"><span data-stu-id="c1277-158">type</span></span> | <span data-ttu-id="c1277-159">The type property of the dataset must be set to: **FileShare**</span><span class="sxs-lookup"><span data-stu-id="c1277-159">The type property of the dataset must be set to: **FileShare**</span></span> |<span data-ttu-id="c1277-160">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-160">Yes</span></span> |
| <span data-ttu-id="c1277-161">folderPath</span><span class="sxs-lookup"><span data-stu-id="c1277-161">folderPath</span></span> | <span data-ttu-id="c1277-162">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="c1277-162">Path to the folder.</span></span> <span data-ttu-id="c1277-163">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="c1277-163">Wildcard filter is not supported.</span></span> <span data-ttu-id="c1277-164">For example: folder/subfolder/</span><span class="sxs-lookup"><span data-stu-id="c1277-164">For example: folder/subfolder/</span></span> |<span data-ttu-id="c1277-165">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-165">Yes</span></span> |
| <span data-ttu-id="c1277-166">fileName</span><span class="sxs-lookup"><span data-stu-id="c1277-166">fileName</span></span> |  <span data-ttu-id="c1277-167">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span><span class="sxs-lookup"><span data-stu-id="c1277-167">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span></span> <span data-ttu-id="c1277-168">If you don't specify a value for this property, the dataset points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="c1277-168">If you don't specify a value for this property, the dataset points to all files in the folder.</span></span> <br/><br/><span data-ttu-id="c1277-169">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span><span class="sxs-lookup"><span data-stu-id="c1277-169">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span></span><br/><span data-ttu-id="c1277-170">- Example 1: `"fileName": "*.csv"`</span><span class="sxs-lookup"><span data-stu-id="c1277-170">- Example 1: `"fileName": "*.csv"`</span></span><br/><span data-ttu-id="c1277-171">- Example 2: `"fileName": "???20180427.txt"`</span><span class="sxs-lookup"><span data-stu-id="c1277-171">- Example 2: `"fileName": "???20180427.txt"`</span></span><br/><span data-ttu-id="c1277-172">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span><span class="sxs-lookup"><span data-stu-id="c1277-172">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span></span> |<span data-ttu-id="c1277-173">No</span><span class="sxs-lookup"><span data-stu-id="c1277-173">No</span></span> |
| <span data-ttu-id="c1277-174">format</span><span class="sxs-lookup"><span data-stu-id="c1277-174">format</span></span> | <span data-ttu-id="c1277-175">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="c1277-175">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="c1277-176">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c1277-176">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c1277-177">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="c1277-177">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c1277-178">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="c1277-178">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="c1277-179">No (only for binary copy scenario)</span><span class="sxs-lookup"><span data-stu-id="c1277-179">No (only for binary copy scenario)</span></span> |
| <span data-ttu-id="c1277-180">compression</span><span class="sxs-lookup"><span data-stu-id="c1277-180">compression</span></span> | <span data-ttu-id="c1277-181">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="c1277-181">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c1277-182">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c1277-182">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="c1277-183">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c1277-183">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="c1277-184">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="c1277-184">Supported levels are: **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="c1277-185">No</span><span class="sxs-lookup"><span data-stu-id="c1277-185">No</span></span> |

>[!TIP]
>To copy all files under a folder, specify **folderPath** only.<br>To copy a single file with a given name, specify **folderPath** with folder part and **fileName** with file name.<br>To copy a subset of files under a folder, specify **folderPath** with folder part and **fileName** with wildcard filter.

<span data-ttu-id="c1277-189">**Example:**</span><span class="sxs-lookup"><span data-stu-id="c1277-189">**Example:**</span></span>

```json
{
    "name": "HDFSDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName":{
            "referenceName": "<HDFS linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "folder/subfolder/",
            "fileName": "myfile.csv.gz",
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

## <a name="copy-activity-properties"></a><span data-ttu-id="c1277-190">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="c1277-190">Copy activity properties</span></span>

<span data-ttu-id="c1277-191">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="c1277-191">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="c1277-192">This section provides a list of properties supported by HDFS source.</span><span class="sxs-lookup"><span data-stu-id="c1277-192">This section provides a list of properties supported by HDFS source.</span></span>

### <a name="hdfs-as-source"></a><span data-ttu-id="c1277-193">HDFS as source</span><span class="sxs-lookup"><span data-stu-id="c1277-193">HDFS as source</span></span>

<span data-ttu-id="c1277-194">To copy data from HDFS, set the source type in the copy activity to **HdfsSource**.</span><span class="sxs-lookup"><span data-stu-id="c1277-194">To copy data from HDFS, set the source type in the copy activity to **HdfsSource**.</span></span> <span data-ttu-id="c1277-195">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="c1277-195">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="c1277-196">Property</span><span class="sxs-lookup"><span data-stu-id="c1277-196">Property</span></span> | <span data-ttu-id="c1277-197">Description</span><span class="sxs-lookup"><span data-stu-id="c1277-197">Description</span></span> | <span data-ttu-id="c1277-198">Required</span><span class="sxs-lookup"><span data-stu-id="c1277-198">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c1277-199">type</span><span class="sxs-lookup"><span data-stu-id="c1277-199">type</span></span> | <span data-ttu-id="c1277-200">The type property of the copy activity source must be set to: **HdfsSource**</span><span class="sxs-lookup"><span data-stu-id="c1277-200">The type property of the copy activity source must be set to: **HdfsSource**</span></span> |<span data-ttu-id="c1277-201">Yes</span><span class="sxs-lookup"><span data-stu-id="c1277-201">Yes</span></span> |
| <span data-ttu-id="c1277-202">recursive</span><span class="sxs-lookup"><span data-stu-id="c1277-202">recursive</span></span> | <span data-ttu-id="c1277-203">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="c1277-203">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> <span data-ttu-id="c1277-204">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span><span class="sxs-lookup"><span data-stu-id="c1277-204">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span></span><br/><span data-ttu-id="c1277-205">Allowed values are: **true** (default), **false**</span><span class="sxs-lookup"><span data-stu-id="c1277-205">Allowed values are: **true** (default), **false**</span></span> | <span data-ttu-id="c1277-206">No</span><span class="sxs-lookup"><span data-stu-id="c1277-206">No</span></span> |
| <span data-ttu-id="c1277-207">distcpSettings</span><span class="sxs-lookup"><span data-stu-id="c1277-207">distcpSettings</span></span> | <span data-ttu-id="c1277-208">Property group when using HDFS DistCp.</span><span class="sxs-lookup"><span data-stu-id="c1277-208">Property group when using HDFS DistCp.</span></span> | <span data-ttu-id="c1277-209">No</span><span class="sxs-lookup"><span data-stu-id="c1277-209">No</span></span> |
| <span data-ttu-id="c1277-210">resourceManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="c1277-210">resourceManagerEndpoint</span></span> | <span data-ttu-id="c1277-211">The Yarn ResourceManager endpoint</span><span class="sxs-lookup"><span data-stu-id="c1277-211">The Yarn ResourceManager endpoint</span></span> | <span data-ttu-id="c1277-212">Yes if using DistCp</span><span class="sxs-lookup"><span data-stu-id="c1277-212">Yes if using DistCp</span></span> |
| <span data-ttu-id="c1277-213">tempScriptPath</span><span class="sxs-lookup"><span data-stu-id="c1277-213">tempScriptPath</span></span> | <span data-ttu-id="c1277-214">A folder path used to store temp DistCp command script.</span><span class="sxs-lookup"><span data-stu-id="c1277-214">A folder path used to store temp DistCp command script.</span></span> <span data-ttu-id="c1277-215">The script file is generated by Data Factory and will be removed after Copy job finished.</span><span class="sxs-lookup"><span data-stu-id="c1277-215">The script file is generated by Data Factory and will be removed after Copy job finished.</span></span> | <span data-ttu-id="c1277-216">Yes if using DistCp</span><span class="sxs-lookup"><span data-stu-id="c1277-216">Yes if using DistCp</span></span> |
| <span data-ttu-id="c1277-217">distcpOptions</span><span class="sxs-lookup"><span data-stu-id="c1277-217">distcpOptions</span></span> | <span data-ttu-id="c1277-218">Additional options provided to DistCp command.</span><span class="sxs-lookup"><span data-stu-id="c1277-218">Additional options provided to DistCp command.</span></span> | <span data-ttu-id="c1277-219">No</span><span class="sxs-lookup"><span data-stu-id="c1277-219">No</span></span> |

<span data-ttu-id="c1277-220">**Example: HDFS source in copy activity using UNLOAD**</span><span class="sxs-lookup"><span data-stu-id="c1277-220">**Example: HDFS source in copy activity using UNLOAD**</span></span>

```json
"source": {
    "type": "HdfsSource",
    "distcpSettings": {
        "resourceManagerEndpoint": "resourcemanagerendpoint:8088",
        "tempScriptPath": "/usr/hadoop/tempscript",
        "distcpOptions": "-m 100"
    }
}
```

<span data-ttu-id="c1277-221">Learn more on how to use DistCp to copy data from HDFS efficiently from the next section.</span><span class="sxs-lookup"><span data-stu-id="c1277-221">Learn more on how to use DistCp to copy data from HDFS efficiently from the next section.</span></span>

## <a name="use-distcp-to-copy-data-from-hdfs"></a><span data-ttu-id="c1277-222">Use DistCp to copy data from HDFS</span><span class="sxs-lookup"><span data-stu-id="c1277-222">Use DistCp to copy data from HDFS</span></span>

<span data-ttu-id="c1277-223">[DistCp](https://hadoop.apache.org/docs/current3/hadoop-distcp/DistCp.html) is a Hadoop native command-line tool to do distributed copy in a Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="c1277-223">[DistCp](https://hadoop.apache.org/docs/current3/hadoop-distcp/DistCp.html) is a Hadoop native command-line tool to do distributed copy in a Hadoop cluster.</span></span> <span data-ttu-id="c1277-224">When run a Distcp command, it will first list all the files to be copied, create several Map jobs into the Hadoop cluster, and each Map job will do binary copy from source to sink.</span><span class="sxs-lookup"><span data-stu-id="c1277-224">When run a Distcp command, it will first list all the files to be copied, create several Map jobs into the Hadoop cluster, and each Map job will do binary copy from source to sink.</span></span>

<span data-ttu-id="c1277-225">Copy Activity support using DistCp to copy files as-is into Azure Blob (including [staged copy](copy-activity-performance.md) or Azure Data Lake Store, in which case it can fully leverage your cluster's power instead of running on the Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="c1277-225">Copy Activity support using DistCp to copy files as-is into Azure Blob (including [staged copy](copy-activity-performance.md) or Azure Data Lake Store, in which case it can fully leverage your cluster's power instead of running on the Self-hosted Integration Runtime.</span></span> <span data-ttu-id="c1277-226">It will provide better copy throughput especially if your cluster is very powerful.</span><span class="sxs-lookup"><span data-stu-id="c1277-226">It will provide better copy throughput especially if your cluster is very powerful.</span></span> <span data-ttu-id="c1277-227">Based on your configuration in Azure Data Factory, Copy activity automatically construct a distcp command, submit to your Hadoop cluster, and monitor the copy status.</span><span class="sxs-lookup"><span data-stu-id="c1277-227">Based on your configuration in Azure Data Factory, Copy activity automatically construct a distcp command, submit to your Hadoop cluster, and monitor the copy status.</span></span>

### <a name="prerequsites"></a><span data-ttu-id="c1277-228">Prerequsites</span><span class="sxs-lookup"><span data-stu-id="c1277-228">Prerequsites</span></span>

<span data-ttu-id="c1277-229">To use DistCp to copy files as-is from HDFS to Azure Blob (including staged copy) or Azure Data Lake Store, make sure your Hadoop cluster meets below requirements:</span><span class="sxs-lookup"><span data-stu-id="c1277-229">To use DistCp to copy files as-is from HDFS to Azure Blob (including staged copy) or Azure Data Lake Store, make sure your Hadoop cluster meets below requirements:</span></span>

1. <span data-ttu-id="c1277-230">MapReduce and Yarn services are enabled.</span><span class="sxs-lookup"><span data-stu-id="c1277-230">MapReduce and Yarn services are enabled.</span></span>
2. <span data-ttu-id="c1277-231">Yarn version is 2.5 or above.</span><span class="sxs-lookup"><span data-stu-id="c1277-231">Yarn version is 2.5 or above.</span></span>
3. <span data-ttu-id="c1277-232">HDFS server is integrated with your target data store - Azure Blob or Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="c1277-232">HDFS server is integrated with your target data store - Azure Blob or Azure Data Lake Store:</span></span>

    - <span data-ttu-id="c1277-233">Azure Blob FileSystem is natively supported since Hadoop 2.7.</span><span class="sxs-lookup"><span data-stu-id="c1277-233">Azure Blob FileSystem is natively supported since Hadoop 2.7.</span></span> <span data-ttu-id="c1277-234">You only need to specify jar path in Hadoop env config.</span><span class="sxs-lookup"><span data-stu-id="c1277-234">You only need to specify jar path in Hadoop env config.</span></span>
    - <span data-ttu-id="c1277-235">Azure Data Lake Store FileSystem is packaged starting from Hadoop 3.0.0-alpha1.</span><span class="sxs-lookup"><span data-stu-id="c1277-235">Azure Data Lake Store FileSystem is packaged starting from Hadoop 3.0.0-alpha1.</span></span> <span data-ttu-id="c1277-236">If your Hadoop cluster is lower than that version, you need to manually import ADLS related jar packages (azure-datalake-store.jar) into cluster from [here](https://hadoop.apache.org/releases.html), and specify jar path in Hadoop env config.</span><span class="sxs-lookup"><span data-stu-id="c1277-236">If your Hadoop cluster is lower than that version, you need to manually import ADLS related jar packages (azure-datalake-store.jar) into cluster from [here](https://hadoop.apache.org/releases.html), and specify jar path in Hadoop env config.</span></span>

4. <span data-ttu-id="c1277-237">Prepare a temp folder in HDFS.</span><span class="sxs-lookup"><span data-stu-id="c1277-237">Prepare a temp folder in HDFS.</span></span> <span data-ttu-id="c1277-238">This temp folder is used to store DistCp shell script, so it will occupy KB-level space.</span><span class="sxs-lookup"><span data-stu-id="c1277-238">This temp folder is used to store DistCp shell script, so it will occupy KB-level space.</span></span>
5. <span data-ttu-id="c1277-239">Make sure the user account provided in HDFS Linked Service have permission to a) submit application in Yarn; b) have the permission to create subfolder, read/write files under above temp folder.</span><span class="sxs-lookup"><span data-stu-id="c1277-239">Make sure the user account provided in HDFS Linked Service have permission to a) submit application in Yarn; b) have the permission to create subfolder, read/write files under above temp folder.</span></span>

### <a name="configurations"></a><span data-ttu-id="c1277-240">Configurations</span><span class="sxs-lookup"><span data-stu-id="c1277-240">Configurations</span></span>

<span data-ttu-id="c1277-241">Below is an example of copy activity configuration to copy data from HDFS to Azure Blob using DistCp:</span><span class="sxs-lookup"><span data-stu-id="c1277-241">Below is an example of copy activity configuration to copy data from HDFS to Azure Blob using DistCp:</span></span>

<span data-ttu-id="c1277-242">**Example:**</span><span class="sxs-lookup"><span data-stu-id="c1277-242">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromHDFSToBlob",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "HDFSDataset",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "BlobDataset",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "HdfsSource",
                "distcpSettings": {
                    "resourceManagerEndpoint": "resourcemanagerendpoint:8088",
                    "tempScriptPath": "/usr/hadoop/tempscript",
                    "distcpOptions": "-strategy dynamic -map 100"
                }
            },
            "sink": {
                "type": "BlobSink"
            }
        }
    }
]
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="c1277-243">Use Kerberos authentication for HDFS connector</span><span class="sxs-lookup"><span data-stu-id="c1277-243">Use Kerberos authentication for HDFS connector</span></span>

<span data-ttu-id="c1277-244">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span><span class="sxs-lookup"><span data-stu-id="c1277-244">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="c1277-245">You can choose the one better fits your case.</span><span class="sxs-lookup"><span data-stu-id="c1277-245">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="c1277-246">Option 1: [Join Self-hosted Integration Runtime machine in Kerberos realm](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="c1277-246">Option 1: [Join Self-hosted Integration Runtime machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="c1277-247">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="c1277-247">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <a name="kerberos-join-realm"></a><span data-ttu-id="c1277-248">Option 1: Join Self-hosted Integration Runtime machine in Kerberos realm</span><span class="sxs-lookup"><span data-stu-id="c1277-248">Option 1: Join Self-hosted Integration Runtime machine in Kerberos realm</span></span>

#### <a name="requirements"></a><span data-ttu-id="c1277-249">Requirements</span><span class="sxs-lookup"><span data-stu-id="c1277-249">Requirements</span></span>

* <span data-ttu-id="c1277-250">The Self-hosted Integration Runtime machine needs to join the Kerberos realm and can’t join any Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c1277-250">The Self-hosted Integration Runtime machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="c1277-251">How to configure</span><span class="sxs-lookup"><span data-stu-id="c1277-251">How to configure</span></span>

<span data-ttu-id="c1277-252">**On Self-hosted Integration Runtime machine:**</span><span class="sxs-lookup"><span data-stu-id="c1277-252">**On Self-hosted Integration Runtime machine:**</span></span>

1.  <span data-ttu-id="c1277-253">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span><span class="sxs-lookup"><span data-stu-id="c1277-253">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="c1277-254">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c1277-254">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="c1277-255">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span><span class="sxs-lookup"><span data-stu-id="c1277-255">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="c1277-256">Replace *REALM.COM* with your own respective realm as needed.</span><span class="sxs-lookup"><span data-stu-id="c1277-256">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="c1277-257">**Restart** the machine after executing these 2 commands.</span><span class="sxs-lookup"><span data-stu-id="c1277-257">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="c1277-258">Verify the configuration with **Ksetup** command.</span><span class="sxs-lookup"><span data-stu-id="c1277-258">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="c1277-259">The output should be like:</span><span class="sxs-lookup"><span data-stu-id="c1277-259">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="c1277-260">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="c1277-260">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="c1277-261">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span><span class="sxs-lookup"><span data-stu-id="c1277-261">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="c1277-262">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span><span class="sxs-lookup"><span data-stu-id="c1277-262">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <a name="kerberos-mutual-trust"></a><span data-ttu-id="c1277-263">Option 2: Enable mutual trust between Windows domain and Kerberos realm</span><span class="sxs-lookup"><span data-stu-id="c1277-263">Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirements"></a><span data-ttu-id="c1277-264">Requirements</span><span class="sxs-lookup"><span data-stu-id="c1277-264">Requirements</span></span>

*   <span data-ttu-id="c1277-265">The Self-hosted Integration Runtime machine must join a Windows domain.</span><span class="sxs-lookup"><span data-stu-id="c1277-265">The Self-hosted Integration Runtime machine must join a Windows domain.</span></span>
*   <span data-ttu-id="c1277-266">You need permission to update the domain controller's settings.</span><span class="sxs-lookup"><span data-stu-id="c1277-266">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="c1277-267">How to configure</span><span class="sxs-lookup"><span data-stu-id="c1277-267">How to configure</span></span>

> [!NOTE]
> Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.

<span data-ttu-id="c1277-269">**On KDC server:**</span><span class="sxs-lookup"><span data-stu-id="c1277-269">**On KDC server:**</span></span>

1.  <span data-ttu-id="c1277-270">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span><span class="sxs-lookup"><span data-stu-id="c1277-270">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="c1277-271">By default, the configuration is located at **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="c1277-271">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="c1277-272">**Restart** the KDC service after configuration.</span><span class="sxs-lookup"><span data-stu-id="c1277-272">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="c1277-273">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span><span class="sxs-lookup"><span data-stu-id="c1277-273">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="c1277-274">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="c1277-274">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="c1277-275">**On domain controller:**</span><span class="sxs-lookup"><span data-stu-id="c1277-275">**On domain controller:**</span></span>

1.  <span data-ttu-id="c1277-276">Run the following **Ksetup** commands to add a realm entry:</span><span class="sxs-lookup"><span data-stu-id="c1277-276">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="c1277-277">Establish trust from Windows Domain to Kerberos Realm.</span><span class="sxs-lookup"><span data-stu-id="c1277-277">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="c1277-278">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="c1277-278">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="c1277-279">Select encryption algorithm used in Kerberos.</span><span class="sxs-lookup"><span data-stu-id="c1277-279">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="c1277-280">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span><span class="sxs-lookup"><span data-stu-id="c1277-280">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="c1277-281">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="c1277-281">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="c1277-282">Select the encryption algorithm you want to use when connect to KDC.</span><span class="sxs-lookup"><span data-stu-id="c1277-282">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="c1277-283">Commonly, you can simply select all the options.</span><span class="sxs-lookup"><span data-stu-id="c1277-283">Commonly, you can simply select all the options.</span></span>

        ![Config Encryption Types for Kerberos](media/connector-hdfs/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="c1277-285">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span><span class="sxs-lookup"><span data-stu-id="c1277-285">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="c1277-286">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span><span class="sxs-lookup"><span data-stu-id="c1277-286">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="c1277-287">Start the Administrative tools > **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="c1277-287">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="c1277-288">Configure advanced features by clicking **View** > **Advanced Features**.</span><span class="sxs-lookup"><span data-stu-id="c1277-288">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="c1277-289">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span><span class="sxs-lookup"><span data-stu-id="c1277-289">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="c1277-290">Add a principal from the realm.</span><span class="sxs-lookup"><span data-stu-id="c1277-290">Add a principal from the realm.</span></span>

        ![Map Security Identity](media/connector-hdfs/map-security-identity.png)

<span data-ttu-id="c1277-292">**On Self-hosted Integration Runtime machine:**</span><span class="sxs-lookup"><span data-stu-id="c1277-292">**On Self-hosted Integration Runtime machine:**</span></span>

* <span data-ttu-id="c1277-293">Run the following **Ksetup** commands to add a realm entry.</span><span class="sxs-lookup"><span data-stu-id="c1277-293">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="c1277-294">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="c1277-294">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="c1277-295">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span><span class="sxs-lookup"><span data-stu-id="c1277-295">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="c1277-296">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span><span class="sxs-lookup"><span data-stu-id="c1277-296">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1277-297">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1277-297">Next steps</span></span>
<span data-ttu-id="c1277-298">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c1277-298">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
