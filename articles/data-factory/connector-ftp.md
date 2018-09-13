---
title: Copy data from an FTP server by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from an FTP server to a supported sink data store by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 05/02/2018
ms.author: jingwang
ms.openlocfilehash: 7a3d776acb06d2aa55f71dafb0ddccbc307f394e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969491"
---
# <a name="copy-data-from-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="7f07a-103">Copy data from FTP server by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7f07a-103">Copy data from FTP server by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-ftp-connector.md)
> * [Current version](connector-ftp.md)

<span data-ttu-id="7f07a-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an FTP server.</span><span class="sxs-lookup"><span data-stu-id="7f07a-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from an FTP server.</span></span> <span data-ttu-id="7f07a-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="7f07a-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="7f07a-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="7f07a-108">Supported capabilities</span></span>

<span data-ttu-id="7f07a-109">You can copy data from FTP server to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="7f07a-109">You can copy data from FTP server to any supported sink data store.</span></span> <span data-ttu-id="7f07a-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="7f07a-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="7f07a-111">Specifically, this FTP connector supports:</span><span class="sxs-lookup"><span data-stu-id="7f07a-111">Specifically, this FTP connector supports:</span></span>

- <span data-ttu-id="7f07a-112">Copying files using **Basic** or **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="7f07a-112">Copying files using **Basic** or **Anonymous** authentication.</span></span>
- <span data-ttu-id="7f07a-113">Copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span><span class="sxs-lookup"><span data-stu-id="7f07a-113">Copying files as-is or parsing files with the [supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="7f07a-114">Get started</span><span class="sxs-lookup"><span data-stu-id="7f07a-114">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="7f07a-115">The following sections provide details about properties that are used to define Data Factory entities specific to FTP.</span><span class="sxs-lookup"><span data-stu-id="7f07a-115">The following sections provide details about properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7f07a-116">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="7f07a-116">Linked service properties</span></span>

<span data-ttu-id="7f07a-117">The following properties are supported for FTP linked service:</span><span class="sxs-lookup"><span data-stu-id="7f07a-117">The following properties are supported for FTP linked service:</span></span>

| <span data-ttu-id="7f07a-118">Property</span><span class="sxs-lookup"><span data-stu-id="7f07a-118">Property</span></span> | <span data-ttu-id="7f07a-119">Description</span><span class="sxs-lookup"><span data-stu-id="7f07a-119">Description</span></span> | <span data-ttu-id="7f07a-120">Required</span><span class="sxs-lookup"><span data-stu-id="7f07a-120">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f07a-121">type</span><span class="sxs-lookup"><span data-stu-id="7f07a-121">type</span></span> | <span data-ttu-id="7f07a-122">The type property must be set to: **FtpServer**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-122">The type property must be set to: **FtpServer**.</span></span> | <span data-ttu-id="7f07a-123">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-123">Yes</span></span> |
| <span data-ttu-id="7f07a-124">host</span><span class="sxs-lookup"><span data-stu-id="7f07a-124">host</span></span> | <span data-ttu-id="7f07a-125">Specify the name or IP address of the FTP server.</span><span class="sxs-lookup"><span data-stu-id="7f07a-125">Specify the name or IP address of the FTP server.</span></span> | <span data-ttu-id="7f07a-126">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-126">Yes</span></span> |
| <span data-ttu-id="7f07a-127">port</span><span class="sxs-lookup"><span data-stu-id="7f07a-127">port</span></span> | <span data-ttu-id="7f07a-128">Specify the port on which the FTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="7f07a-128">Specify the port on which the FTP server is listening.</span></span><br/><span data-ttu-id="7f07a-129">Allowed values are: integer, default value is **21**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-129">Allowed values are: integer, default value is **21**.</span></span> | <span data-ttu-id="7f07a-130">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-130">No</span></span> |
| <span data-ttu-id="7f07a-131">enableSsl</span><span class="sxs-lookup"><span data-stu-id="7f07a-131">enableSsl</span></span> | <span data-ttu-id="7f07a-132">Specify whether to use FTP over an SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="7f07a-132">Specify whether to use FTP over an SSL/TLS channel.</span></span><br/><span data-ttu-id="7f07a-133">Allowed values are: **true** (default), **false**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-133">Allowed values are: **true** (default), **false**.</span></span> | <span data-ttu-id="7f07a-134">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-134">No</span></span> |
| <span data-ttu-id="7f07a-135">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="7f07a-135">enableServerCertificateValidation</span></span> | <span data-ttu-id="7f07a-136">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span><span class="sxs-lookup"><span data-stu-id="7f07a-136">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span><br/><span data-ttu-id="7f07a-137">Allowed values are: **true** (default), **false**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-137">Allowed values are: **true** (default), **false**.</span></span> | <span data-ttu-id="7f07a-138">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-138">No</span></span> |
| <span data-ttu-id="7f07a-139">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7f07a-139">authenticationType</span></span> | <span data-ttu-id="7f07a-140">Specify the authentication type.</span><span class="sxs-lookup"><span data-stu-id="7f07a-140">Specify the authentication type.</span></span><br/><span data-ttu-id="7f07a-141">Allowed values are: **Basic**, **Anonymous**</span><span class="sxs-lookup"><span data-stu-id="7f07a-141">Allowed values are: **Basic**, **Anonymous**</span></span> | <span data-ttu-id="7f07a-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-142">Yes</span></span> |
| <span data-ttu-id="7f07a-143">userName</span><span class="sxs-lookup"><span data-stu-id="7f07a-143">userName</span></span> | <span data-ttu-id="7f07a-144">Specify the user who has access to the FTP server.</span><span class="sxs-lookup"><span data-stu-id="7f07a-144">Specify the user who has access to the FTP server.</span></span> | <span data-ttu-id="7f07a-145">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-145">No</span></span> |
| <span data-ttu-id="7f07a-146">password</span><span class="sxs-lookup"><span data-stu-id="7f07a-146">password</span></span> | <span data-ttu-id="7f07a-147">Specify the password for the user (userName).</span><span class="sxs-lookup"><span data-stu-id="7f07a-147">Specify the password for the user (userName).</span></span> <span data-ttu-id="7f07a-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7f07a-148">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="7f07a-149">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-149">No</span></span> |
| <span data-ttu-id="7f07a-150">connectVia</span><span class="sxs-lookup"><span data-stu-id="7f07a-150">connectVia</span></span> | <span data-ttu-id="7f07a-151">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="7f07a-151">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="7f07a-152">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="7f07a-152">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="7f07a-153">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="7f07a-153">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="7f07a-154">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-154">No</span></span> |

>[!NOTE]
>The FTP connector supports accessing FTP server with either no encryption or explicit SSL/TLS encryption; it doesn’t support implicit SSL/TLS encryption.

<span data-ttu-id="7f07a-156">**Example 1: using Anonymous authentication**</span><span class="sxs-lookup"><span data-stu-id="7f07a-156">**Example 1: using Anonymous authentication**</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "<ftp server>",
            "port": 21,
            "enableSsl": true,
            "enableServerCertificateValidation": true,
            "authenticationType": "Anonymous"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="7f07a-157">**Example 2: using Basic authentication**</span><span class="sxs-lookup"><span data-stu-id="7f07a-157">**Example 2: using Basic authentication**</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "<ftp server>",
            "port": 21,
            "enableSsl": true,
            "enableServerCertificateValidation": true,
            "authenticationType": "Basic",
            "userName": "<username>",
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

## <a name="dataset-properties"></a><span data-ttu-id="7f07a-158">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="7f07a-158">Dataset properties</span></span>

<span data-ttu-id="7f07a-159">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="7f07a-159">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="7f07a-160">This section provides a list of properties supported by FTP dataset.</span><span class="sxs-lookup"><span data-stu-id="7f07a-160">This section provides a list of properties supported by FTP dataset.</span></span>

<span data-ttu-id="7f07a-161">To copy data from FTP, set the type property of the dataset to **FileShare**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-161">To copy data from FTP, set the type property of the dataset to **FileShare**.</span></span> <span data-ttu-id="7f07a-162">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="7f07a-162">The following properties are supported:</span></span>

| <span data-ttu-id="7f07a-163">Property</span><span class="sxs-lookup"><span data-stu-id="7f07a-163">Property</span></span> | <span data-ttu-id="7f07a-164">Description</span><span class="sxs-lookup"><span data-stu-id="7f07a-164">Description</span></span> | <span data-ttu-id="7f07a-165">Required</span><span class="sxs-lookup"><span data-stu-id="7f07a-165">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f07a-166">type</span><span class="sxs-lookup"><span data-stu-id="7f07a-166">type</span></span> | <span data-ttu-id="7f07a-167">The type property of the dataset must be set to: **FileShare**</span><span class="sxs-lookup"><span data-stu-id="7f07a-167">The type property of the dataset must be set to: **FileShare**</span></span> |<span data-ttu-id="7f07a-168">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-168">Yes</span></span> |
| <span data-ttu-id="7f07a-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="7f07a-169">folderPath</span></span> | <span data-ttu-id="7f07a-170">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="7f07a-170">Path to the folder.</span></span> <span data-ttu-id="7f07a-171">Wildcard filter is not supported.</span><span class="sxs-lookup"><span data-stu-id="7f07a-171">Wildcard filter is not supported.</span></span> <span data-ttu-id="7f07a-172">For example: folder/subfolder/</span><span class="sxs-lookup"><span data-stu-id="7f07a-172">For example: folder/subfolder/</span></span> |<span data-ttu-id="7f07a-173">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-173">Yes</span></span> |
| <span data-ttu-id="7f07a-174">fileName</span><span class="sxs-lookup"><span data-stu-id="7f07a-174">fileName</span></span> | <span data-ttu-id="7f07a-175">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span><span class="sxs-lookup"><span data-stu-id="7f07a-175">**Name or wildcard filter** for the file(s) under the specified "folderPath".</span></span> <span data-ttu-id="7f07a-176">If you don't specify a value for this property, the dataset points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="7f07a-176">If you don't specify a value for this property, the dataset points to all files in the folder.</span></span> <br/><br/><span data-ttu-id="7f07a-177">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span><span class="sxs-lookup"><span data-stu-id="7f07a-177">For filter, allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character).</span></span><br/><span data-ttu-id="7f07a-178">- Example 1: `"fileName": "*.csv"`</span><span class="sxs-lookup"><span data-stu-id="7f07a-178">- Example 1: `"fileName": "*.csv"`</span></span><br/><span data-ttu-id="7f07a-179">- Example 2: `"fileName": "???20180427.txt"`</span><span class="sxs-lookup"><span data-stu-id="7f07a-179">- Example 2: `"fileName": "???20180427.txt"`</span></span><br/><span data-ttu-id="7f07a-180">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span><span class="sxs-lookup"><span data-stu-id="7f07a-180">Use `^` to escape if your actual file name has wildcard or this escape char inside.</span></span> |<span data-ttu-id="7f07a-181">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-181">No</span></span> |
| <span data-ttu-id="7f07a-182">format</span><span class="sxs-lookup"><span data-stu-id="7f07a-182">format</span></span> | <span data-ttu-id="7f07a-183">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="7f07a-183">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span><br/><br/><span data-ttu-id="7f07a-184">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-184">If you want to parse files with a specific format, the following file format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="7f07a-185">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="7f07a-185">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="7f07a-186">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="7f07a-186">For more information, see [Text Format](supported-file-formats-and-compression-codecs.md#text-format), [Json Format](supported-file-formats-and-compression-codecs.md#json-format), [Avro Format](supported-file-formats-and-compression-codecs.md#avro-format), [Orc Format](supported-file-formats-and-compression-codecs.md#orc-format), and [Parquet Format](supported-file-formats-and-compression-codecs.md#parquet-format) sections.</span></span> |<span data-ttu-id="7f07a-187">No (only for binary copy scenario)</span><span class="sxs-lookup"><span data-stu-id="7f07a-187">No (only for binary copy scenario)</span></span> |
| <span data-ttu-id="7f07a-188">compression</span><span class="sxs-lookup"><span data-stu-id="7f07a-188">compression</span></span> | <span data-ttu-id="7f07a-189">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="7f07a-189">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="7f07a-190">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="7f07a-190">For more information, see [Supported file formats and compression codecs](supported-file-formats-and-compression-codecs.md#compression-support).</span></span><br/><span data-ttu-id="7f07a-191">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-191">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span><br/><span data-ttu-id="7f07a-192">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-192">Supported levels are: **Optimal** and **Fastest**.</span></span> |<span data-ttu-id="7f07a-193">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-193">No</span></span> |
| <span data-ttu-id="7f07a-194">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="7f07a-194">useBinaryTransfer</span></span> | <span data-ttu-id="7f07a-195">Specify whether to use the binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="7f07a-195">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="7f07a-196">The values are true for binary mode (default), and false for ASCII.</span><span class="sxs-lookup"><span data-stu-id="7f07a-196">The values are true for binary mode (default), and false for ASCII.</span></span> |<span data-ttu-id="7f07a-197">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-197">No</span></span> |

>[!TIP]
>To copy all files under a folder, specify **folderPath** only.<br>To copy a single file with a given name, specify **folderPath** with folder part and **fileName** with file name.<br>To copy a subset of files under a folder, specify **folderPath** with folder part and **fileName** with wildcard filter.

>[!NOTE]
>If you were using "fileFilter" property for file filter, it is still supported as-is, while you are suggested to use the new filter capability added to "fileName" going forward.

<span data-ttu-id="7f07a-202">**Example:**</span><span class="sxs-lookup"><span data-stu-id="7f07a-202">**Example:**</span></span>

```json
{
    "name": "FTPDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName":{
            "referenceName": "<FTP linked service name>",
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

## <a name="copy-activity-properties"></a><span data-ttu-id="7f07a-203">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="7f07a-203">Copy activity properties</span></span>

<span data-ttu-id="7f07a-204">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="7f07a-204">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="7f07a-205">This section provides a list of properties supported by FTP source.</span><span class="sxs-lookup"><span data-stu-id="7f07a-205">This section provides a list of properties supported by FTP source.</span></span>

### <a name="ftp-as-source"></a><span data-ttu-id="7f07a-206">FTP as source</span><span class="sxs-lookup"><span data-stu-id="7f07a-206">FTP as source</span></span>

<span data-ttu-id="7f07a-207">To copy data from FTP, set the source type in the copy activity to **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="7f07a-207">To copy data from FTP, set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="7f07a-208">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="7f07a-208">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="7f07a-209">Property</span><span class="sxs-lookup"><span data-stu-id="7f07a-209">Property</span></span> | <span data-ttu-id="7f07a-210">Description</span><span class="sxs-lookup"><span data-stu-id="7f07a-210">Description</span></span> | <span data-ttu-id="7f07a-211">Required</span><span class="sxs-lookup"><span data-stu-id="7f07a-211">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f07a-212">type</span><span class="sxs-lookup"><span data-stu-id="7f07a-212">type</span></span> | <span data-ttu-id="7f07a-213">The type property of the copy activity source must be set to: **FileSystemSource**</span><span class="sxs-lookup"><span data-stu-id="7f07a-213">The type property of the copy activity source must be set to: **FileSystemSource**</span></span> |<span data-ttu-id="7f07a-214">Yes</span><span class="sxs-lookup"><span data-stu-id="7f07a-214">Yes</span></span> |
| <span data-ttu-id="7f07a-215">recursive</span><span class="sxs-lookup"><span data-stu-id="7f07a-215">recursive</span></span> | <span data-ttu-id="7f07a-216">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="7f07a-216">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> <span data-ttu-id="7f07a-217">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span><span class="sxs-lookup"><span data-stu-id="7f07a-217">Note when recursive is set to true and sink is file-based store, empty folder/sub-folder will not be copied/created at sink.</span></span><br/><span data-ttu-id="7f07a-218">Allowed values are: **true** (default), **false**</span><span class="sxs-lookup"><span data-stu-id="7f07a-218">Allowed values are: **true** (default), **false**</span></span> | <span data-ttu-id="7f07a-219">No</span><span class="sxs-lookup"><span data-stu-id="7f07a-219">No</span></span> |

<span data-ttu-id="7f07a-220">**Example:**</span><span class="sxs-lookup"><span data-stu-id="7f07a-220">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromFTP",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<FTP input dataset name>",
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


## <a name="next-steps"></a><span data-ttu-id="7f07a-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f07a-221">Next steps</span></span>
<span data-ttu-id="7f07a-222">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7f07a-222">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
