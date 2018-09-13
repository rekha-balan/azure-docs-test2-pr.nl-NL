---
title: Copy data from Teradata using Azure Data Factory | Microsoft Docs
description: Learn about Teradata Connector of the Data Factory service that lets you copy data from Teradata database to data stores supported by Data Factory as sinks.
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
ms.openlocfilehash: a2928b202f56674c69e6431201db6d846a9feb9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855628"
---
# <a name="copy-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="005ca-103">Copy data from Teradata using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="005ca-103">Copy data from Teradata using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-teradata-connector.md)
> * [Current version](connector-teradata.md)

<span data-ttu-id="005ca-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Teradata database.</span><span class="sxs-lookup"><span data-stu-id="005ca-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Teradata database.</span></span> <span data-ttu-id="005ca-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="005ca-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="005ca-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="005ca-108">Supported capabilities</span></span>

<span data-ttu-id="005ca-109">You can copy data from Teradata database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="005ca-109">You can copy data from Teradata database to any supported sink data store.</span></span> <span data-ttu-id="005ca-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="005ca-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="005ca-111">Specifically, this Teradata connector supports:</span><span class="sxs-lookup"><span data-stu-id="005ca-111">Specifically, this Teradata connector supports:</span></span>

- <span data-ttu-id="005ca-112">Teradata **version 12 and above**.</span><span class="sxs-lookup"><span data-stu-id="005ca-112">Teradata **version 12 and above**.</span></span>
- <span data-ttu-id="005ca-113">Copying data using **Basic** or **Windows** authentication.</span><span class="sxs-lookup"><span data-stu-id="005ca-113">Copying data using **Basic** or **Windows** authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="005ca-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="005ca-114">Prerequisites</span></span>

<span data-ttu-id="005ca-115">To use this Teradata connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="005ca-115">To use this Teradata connector, you need to:</span></span>

- <span data-ttu-id="005ca-116">Set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="005ca-116">Set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="005ca-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="005ca-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>
- <span data-ttu-id="005ca-118">Install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="005ca-118">Install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the Integration Runtime machine.</span></span>

## <a name="getting-started"></a><span data-ttu-id="005ca-119">Getting started</span><span class="sxs-lookup"><span data-stu-id="005ca-119">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="005ca-120">The following sections provide details about properties that are used to define Data Factory entities specific to Teradata connector.</span><span class="sxs-lookup"><span data-stu-id="005ca-120">The following sections provide details about properties that are used to define Data Factory entities specific to Teradata connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="005ca-121">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="005ca-121">Linked service properties</span></span>

<span data-ttu-id="005ca-122">The following properties are supported for Teradata linked service:</span><span class="sxs-lookup"><span data-stu-id="005ca-122">The following properties are supported for Teradata linked service:</span></span>

| <span data-ttu-id="005ca-123">Property</span><span class="sxs-lookup"><span data-stu-id="005ca-123">Property</span></span> | <span data-ttu-id="005ca-124">Description</span><span class="sxs-lookup"><span data-stu-id="005ca-124">Description</span></span> | <span data-ttu-id="005ca-125">Required</span><span class="sxs-lookup"><span data-stu-id="005ca-125">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="005ca-126">type</span><span class="sxs-lookup"><span data-stu-id="005ca-126">type</span></span> | <span data-ttu-id="005ca-127">The type property must be set to: **Teradata**</span><span class="sxs-lookup"><span data-stu-id="005ca-127">The type property must be set to: **Teradata**</span></span> | <span data-ttu-id="005ca-128">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-128">Yes</span></span> |
| <span data-ttu-id="005ca-129">server</span><span class="sxs-lookup"><span data-stu-id="005ca-129">server</span></span> | <span data-ttu-id="005ca-130">Name of the Teradata server.</span><span class="sxs-lookup"><span data-stu-id="005ca-130">Name of the Teradata server.</span></span> | <span data-ttu-id="005ca-131">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-131">Yes</span></span> |
| <span data-ttu-id="005ca-132">authenticationType</span><span class="sxs-lookup"><span data-stu-id="005ca-132">authenticationType</span></span> | <span data-ttu-id="005ca-133">Type of authentication used to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="005ca-133">Type of authentication used to connect to the Teradata database.</span></span><br/><span data-ttu-id="005ca-134">Allowed values are: **Basic**, and **Windows**.</span><span class="sxs-lookup"><span data-stu-id="005ca-134">Allowed values are: **Basic**, and **Windows**.</span></span> | <span data-ttu-id="005ca-135">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-135">Yes</span></span> |
| <span data-ttu-id="005ca-136">username</span><span class="sxs-lookup"><span data-stu-id="005ca-136">username</span></span> | <span data-ttu-id="005ca-137">Specify user name to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="005ca-137">Specify user name to connect to the Teradata database.</span></span> | <span data-ttu-id="005ca-138">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-138">Yes</span></span> |
| <span data-ttu-id="005ca-139">password</span><span class="sxs-lookup"><span data-stu-id="005ca-139">password</span></span> | <span data-ttu-id="005ca-140">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="005ca-140">Specify password for the user account you specified for the username.</span></span> <span data-ttu-id="005ca-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="005ca-141">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="005ca-142">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-142">Yes</span></span> |
| <span data-ttu-id="005ca-143">connectVia</span><span class="sxs-lookup"><span data-stu-id="005ca-143">connectVia</span></span> | <span data-ttu-id="005ca-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="005ca-144">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="005ca-145">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="005ca-145">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="005ca-146">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-146">Yes</span></span> |

<span data-ttu-id="005ca-147">**Example:**</span><span class="sxs-lookup"><span data-stu-id="005ca-147">**Example:**</span></span>

```json
{
    "name": "TeradataLinkedService",
    "properties": {
        "type": "Teradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "Basic",
            "username": "<username>",
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

## <a name="dataset-properties"></a><span data-ttu-id="005ca-148">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="005ca-148">Dataset properties</span></span>

<span data-ttu-id="005ca-149">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="005ca-149">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="005ca-150">This section provides a list of properties supported by Teradata dataset.</span><span class="sxs-lookup"><span data-stu-id="005ca-150">This section provides a list of properties supported by Teradata dataset.</span></span>

<span data-ttu-id="005ca-151">To copy data from Teradata, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="005ca-151">To copy data from Teradata, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="005ca-152">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="005ca-152">The following properties are supported:</span></span>

| <span data-ttu-id="005ca-153">Property</span><span class="sxs-lookup"><span data-stu-id="005ca-153">Property</span></span> | <span data-ttu-id="005ca-154">Description</span><span class="sxs-lookup"><span data-stu-id="005ca-154">Description</span></span> | <span data-ttu-id="005ca-155">Required</span><span class="sxs-lookup"><span data-stu-id="005ca-155">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="005ca-156">type</span><span class="sxs-lookup"><span data-stu-id="005ca-156">type</span></span> | <span data-ttu-id="005ca-157">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="005ca-157">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="005ca-158">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-158">Yes</span></span> |
| <span data-ttu-id="005ca-159">tableName</span><span class="sxs-lookup"><span data-stu-id="005ca-159">tableName</span></span> | <span data-ttu-id="005ca-160">Name of the table in the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="005ca-160">Name of the table in the Teradata database.</span></span> | <span data-ttu-id="005ca-161">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="005ca-161">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="005ca-162">**Example:**</span><span class="sxs-lookup"><span data-stu-id="005ca-162">**Example:**</span></span>

```json
{
    "name": "TeradataDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<Teradata linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="005ca-163">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="005ca-163">Copy activity properties</span></span>

<span data-ttu-id="005ca-164">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="005ca-164">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="005ca-165">This section provides a list of properties supported by Teradata source.</span><span class="sxs-lookup"><span data-stu-id="005ca-165">This section provides a list of properties supported by Teradata source.</span></span>

### <a name="teradata-as-source"></a><span data-ttu-id="005ca-166">Teradata as source</span><span class="sxs-lookup"><span data-stu-id="005ca-166">Teradata as source</span></span>

<span data-ttu-id="005ca-167">To copy data from Teradata, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="005ca-167">To copy data from Teradata, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="005ca-168">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="005ca-168">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="005ca-169">Property</span><span class="sxs-lookup"><span data-stu-id="005ca-169">Property</span></span> | <span data-ttu-id="005ca-170">Description</span><span class="sxs-lookup"><span data-stu-id="005ca-170">Description</span></span> | <span data-ttu-id="005ca-171">Required</span><span class="sxs-lookup"><span data-stu-id="005ca-171">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="005ca-172">type</span><span class="sxs-lookup"><span data-stu-id="005ca-172">type</span></span> | <span data-ttu-id="005ca-173">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="005ca-173">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="005ca-174">Yes</span><span class="sxs-lookup"><span data-stu-id="005ca-174">Yes</span></span> |
| <span data-ttu-id="005ca-175">query</span><span class="sxs-lookup"><span data-stu-id="005ca-175">query</span></span> | <span data-ttu-id="005ca-176">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="005ca-176">Use the custom SQL query to read data.</span></span> <span data-ttu-id="005ca-177">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="005ca-177">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="005ca-178">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="005ca-178">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="005ca-179">**Example:**</span><span class="sxs-lookup"><span data-stu-id="005ca-179">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromTeradata",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Teradata input dataset name>",
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
                "type": "RelationalSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-teradata"></a><span data-ttu-id="005ca-180">Data type mapping for Teradata</span><span class="sxs-lookup"><span data-stu-id="005ca-180">Data type mapping for Teradata</span></span>

<span data-ttu-id="005ca-181">When copying data from Teradata, the following mappings are used from Teradata data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="005ca-181">When copying data from Teradata, the following mappings are used from Teradata data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="005ca-182">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="005ca-182">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="005ca-183">Teradata data type</span><span class="sxs-lookup"><span data-stu-id="005ca-183">Teradata data type</span></span> | <span data-ttu-id="005ca-184">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="005ca-184">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="005ca-185">BigInt</span><span class="sxs-lookup"><span data-stu-id="005ca-185">BigInt</span></span> |<span data-ttu-id="005ca-186">Int64</span><span class="sxs-lookup"><span data-stu-id="005ca-186">Int64</span></span> |
| <span data-ttu-id="005ca-187">Blob</span><span class="sxs-lookup"><span data-stu-id="005ca-187">Blob</span></span> |<span data-ttu-id="005ca-188">Byte[]</span><span class="sxs-lookup"><span data-stu-id="005ca-188">Byte[]</span></span> |
| <span data-ttu-id="005ca-189">Byte</span><span class="sxs-lookup"><span data-stu-id="005ca-189">Byte</span></span> |<span data-ttu-id="005ca-190">Byte[]</span><span class="sxs-lookup"><span data-stu-id="005ca-190">Byte[]</span></span> |
| <span data-ttu-id="005ca-191">ByteInt</span><span class="sxs-lookup"><span data-stu-id="005ca-191">ByteInt</span></span> |<span data-ttu-id="005ca-192">Int16</span><span class="sxs-lookup"><span data-stu-id="005ca-192">Int16</span></span> |
| <span data-ttu-id="005ca-193">Char</span><span class="sxs-lookup"><span data-stu-id="005ca-193">Char</span></span> |<span data-ttu-id="005ca-194">String</span><span class="sxs-lookup"><span data-stu-id="005ca-194">String</span></span> |
| <span data-ttu-id="005ca-195">Clob</span><span class="sxs-lookup"><span data-stu-id="005ca-195">Clob</span></span> |<span data-ttu-id="005ca-196">String</span><span class="sxs-lookup"><span data-stu-id="005ca-196">String</span></span> |
| <span data-ttu-id="005ca-197">Date</span><span class="sxs-lookup"><span data-stu-id="005ca-197">Date</span></span> |<span data-ttu-id="005ca-198">DateTime</span><span class="sxs-lookup"><span data-stu-id="005ca-198">DateTime</span></span> |
| <span data-ttu-id="005ca-199">Decimal</span><span class="sxs-lookup"><span data-stu-id="005ca-199">Decimal</span></span> |<span data-ttu-id="005ca-200">Decimal</span><span class="sxs-lookup"><span data-stu-id="005ca-200">Decimal</span></span> |
| <span data-ttu-id="005ca-201">Double</span><span class="sxs-lookup"><span data-stu-id="005ca-201">Double</span></span> |<span data-ttu-id="005ca-202">Double</span><span class="sxs-lookup"><span data-stu-id="005ca-202">Double</span></span> |
| <span data-ttu-id="005ca-203">Graphic</span><span class="sxs-lookup"><span data-stu-id="005ca-203">Graphic</span></span> |<span data-ttu-id="005ca-204">String</span><span class="sxs-lookup"><span data-stu-id="005ca-204">String</span></span> |
| <span data-ttu-id="005ca-205">Integer</span><span class="sxs-lookup"><span data-stu-id="005ca-205">Integer</span></span> |<span data-ttu-id="005ca-206">Int32</span><span class="sxs-lookup"><span data-stu-id="005ca-206">Int32</span></span> |
| <span data-ttu-id="005ca-207">Interval Day</span><span class="sxs-lookup"><span data-stu-id="005ca-207">Interval Day</span></span> |<span data-ttu-id="005ca-208">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-208">TimeSpan</span></span> |
| <span data-ttu-id="005ca-209">Interval Day To Hour</span><span class="sxs-lookup"><span data-stu-id="005ca-209">Interval Day To Hour</span></span> |<span data-ttu-id="005ca-210">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-210">TimeSpan</span></span> |
| <span data-ttu-id="005ca-211">Interval Day To Minute</span><span class="sxs-lookup"><span data-stu-id="005ca-211">Interval Day To Minute</span></span> |<span data-ttu-id="005ca-212">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-212">TimeSpan</span></span> |
| <span data-ttu-id="005ca-213">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="005ca-213">Interval Day To Second</span></span> |<span data-ttu-id="005ca-214">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-214">TimeSpan</span></span> |
| <span data-ttu-id="005ca-215">Interval Hour</span><span class="sxs-lookup"><span data-stu-id="005ca-215">Interval Hour</span></span> |<span data-ttu-id="005ca-216">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-216">TimeSpan</span></span> |
| <span data-ttu-id="005ca-217">Interval Hour To Minute</span><span class="sxs-lookup"><span data-stu-id="005ca-217">Interval Hour To Minute</span></span> |<span data-ttu-id="005ca-218">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-218">TimeSpan</span></span> |
| <span data-ttu-id="005ca-219">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="005ca-219">Interval Hour To Second</span></span> |<span data-ttu-id="005ca-220">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-220">TimeSpan</span></span> |
| <span data-ttu-id="005ca-221">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="005ca-221">Interval Minute</span></span> |<span data-ttu-id="005ca-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-222">TimeSpan</span></span> |
| <span data-ttu-id="005ca-223">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="005ca-223">Interval Minute To Second</span></span> |<span data-ttu-id="005ca-224">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-224">TimeSpan</span></span> |
| <span data-ttu-id="005ca-225">Interval Month</span><span class="sxs-lookup"><span data-stu-id="005ca-225">Interval Month</span></span> |<span data-ttu-id="005ca-226">String</span><span class="sxs-lookup"><span data-stu-id="005ca-226">String</span></span> |
| <span data-ttu-id="005ca-227">Interval Second</span><span class="sxs-lookup"><span data-stu-id="005ca-227">Interval Second</span></span> |<span data-ttu-id="005ca-228">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-228">TimeSpan</span></span> |
| <span data-ttu-id="005ca-229">Interval Year</span><span class="sxs-lookup"><span data-stu-id="005ca-229">Interval Year</span></span> |<span data-ttu-id="005ca-230">String</span><span class="sxs-lookup"><span data-stu-id="005ca-230">String</span></span> |
| <span data-ttu-id="005ca-231">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="005ca-231">Interval Year To Month</span></span> |<span data-ttu-id="005ca-232">String</span><span class="sxs-lookup"><span data-stu-id="005ca-232">String</span></span> |
| <span data-ttu-id="005ca-233">Number</span><span class="sxs-lookup"><span data-stu-id="005ca-233">Number</span></span> |<span data-ttu-id="005ca-234">Double</span><span class="sxs-lookup"><span data-stu-id="005ca-234">Double</span></span> |
| <span data-ttu-id="005ca-235">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="005ca-235">Period(Date)</span></span> |<span data-ttu-id="005ca-236">String</span><span class="sxs-lookup"><span data-stu-id="005ca-236">String</span></span> |
| <span data-ttu-id="005ca-237">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="005ca-237">Period(Time)</span></span> |<span data-ttu-id="005ca-238">String</span><span class="sxs-lookup"><span data-stu-id="005ca-238">String</span></span> |
| <span data-ttu-id="005ca-239">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="005ca-239">Period(Time With Time Zone)</span></span> |<span data-ttu-id="005ca-240">String</span><span class="sxs-lookup"><span data-stu-id="005ca-240">String</span></span> |
| <span data-ttu-id="005ca-241">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="005ca-241">Period(Timestamp)</span></span> |<span data-ttu-id="005ca-242">String</span><span class="sxs-lookup"><span data-stu-id="005ca-242">String</span></span> |
| <span data-ttu-id="005ca-243">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="005ca-243">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="005ca-244">String</span><span class="sxs-lookup"><span data-stu-id="005ca-244">String</span></span> |
| <span data-ttu-id="005ca-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="005ca-245">SmallInt</span></span> |<span data-ttu-id="005ca-246">Int16</span><span class="sxs-lookup"><span data-stu-id="005ca-246">Int16</span></span> |
| <span data-ttu-id="005ca-247">Time</span><span class="sxs-lookup"><span data-stu-id="005ca-247">Time</span></span> |<span data-ttu-id="005ca-248">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="005ca-248">TimeSpan</span></span> |
| <span data-ttu-id="005ca-249">Time With Time Zone</span><span class="sxs-lookup"><span data-stu-id="005ca-249">Time With Time Zone</span></span> |<span data-ttu-id="005ca-250">String</span><span class="sxs-lookup"><span data-stu-id="005ca-250">String</span></span> |
| <span data-ttu-id="005ca-251">Timestamp</span><span class="sxs-lookup"><span data-stu-id="005ca-251">Timestamp</span></span> |<span data-ttu-id="005ca-252">DateTime</span><span class="sxs-lookup"><span data-stu-id="005ca-252">DateTime</span></span> |
| <span data-ttu-id="005ca-253">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="005ca-253">Timestamp With Time Zone</span></span> |<span data-ttu-id="005ca-254">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="005ca-254">DateTimeOffset</span></span> |
| <span data-ttu-id="005ca-255">VarByte</span><span class="sxs-lookup"><span data-stu-id="005ca-255">VarByte</span></span> |<span data-ttu-id="005ca-256">Byte[]</span><span class="sxs-lookup"><span data-stu-id="005ca-256">Byte[]</span></span> |
| <span data-ttu-id="005ca-257">VarChar</span><span class="sxs-lookup"><span data-stu-id="005ca-257">VarChar</span></span> |<span data-ttu-id="005ca-258">String</span><span class="sxs-lookup"><span data-stu-id="005ca-258">String</span></span> |
| <span data-ttu-id="005ca-259">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="005ca-259">VarGraphic</span></span> |<span data-ttu-id="005ca-260">String</span><span class="sxs-lookup"><span data-stu-id="005ca-260">String</span></span> |
| <span data-ttu-id="005ca-261">Xml</span><span class="sxs-lookup"><span data-stu-id="005ca-261">Xml</span></span> |<span data-ttu-id="005ca-262">String</span><span class="sxs-lookup"><span data-stu-id="005ca-262">String</span></span> |


## <a name="next-steps"></a><span data-ttu-id="005ca-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="005ca-263">Next steps</span></span>
<span data-ttu-id="005ca-264">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="005ca-264">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
