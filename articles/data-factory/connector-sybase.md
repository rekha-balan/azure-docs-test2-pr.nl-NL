---
title: Copy data from Sybase using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Sybase to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 0eb74cee8fb1f4c5d301693a4d53e5d564e12a00
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869247"
---
# <a name="copy-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="cbb60-103">Copy data from Sybase using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cbb60-103">Copy data from Sybase using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-sybase-connector.md)
> * [Current version](connector-sybase.md)

<span data-ttu-id="cbb60-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Sybase database.</span><span class="sxs-lookup"><span data-stu-id="cbb60-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Sybase database.</span></span> <span data-ttu-id="cbb60-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="cbb60-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="cbb60-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="cbb60-108">Supported capabilities</span></span>

<span data-ttu-id="cbb60-109">You can copy data from Sybase database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="cbb60-109">You can copy data from Sybase database to any supported sink data store.</span></span> <span data-ttu-id="cbb60-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="cbb60-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="cbb60-111">Specifically, this Sybase connector supports:</span><span class="sxs-lookup"><span data-stu-id="cbb60-111">Specifically, this Sybase connector supports:</span></span>

- <span data-ttu-id="cbb60-112">SAP Sybase SQL Anywhere (ASA) **version 16 and above**; IQ and ASE are not supported.</span><span class="sxs-lookup"><span data-stu-id="cbb60-112">SAP Sybase SQL Anywhere (ASA) **version 16 and above**; IQ and ASE are not supported.</span></span>
- <span data-ttu-id="cbb60-113">Copying data using **Basic** or **Windows** authentication.</span><span class="sxs-lookup"><span data-stu-id="cbb60-113">Copying data using **Basic** or **Windows** authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbb60-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cbb60-114">Prerequisites</span></span>

<span data-ttu-id="cbb60-115">To use this Sybase connector, you need to:</span><span class="sxs-lookup"><span data-stu-id="cbb60-115">To use this Sybase connector, you need to:</span></span>

- <span data-ttu-id="cbb60-116">Set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="cbb60-116">Set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="cbb60-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="cbb60-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>
- <span data-ttu-id="cbb60-118">Install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="cbb60-118">Install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the Integration Runtime machine.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cbb60-119">Getting started</span><span class="sxs-lookup"><span data-stu-id="cbb60-119">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="cbb60-120">The following sections provide details about properties that are used to define Data Factory entities specific to Sybase connector.</span><span class="sxs-lookup"><span data-stu-id="cbb60-120">The following sections provide details about properties that are used to define Data Factory entities specific to Sybase connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cbb60-121">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="cbb60-121">Linked service properties</span></span>

<span data-ttu-id="cbb60-122">The following properties are supported for Sybase linked service:</span><span class="sxs-lookup"><span data-stu-id="cbb60-122">The following properties are supported for Sybase linked service:</span></span>

| <span data-ttu-id="cbb60-123">Property</span><span class="sxs-lookup"><span data-stu-id="cbb60-123">Property</span></span> | <span data-ttu-id="cbb60-124">Description</span><span class="sxs-lookup"><span data-stu-id="cbb60-124">Description</span></span> | <span data-ttu-id="cbb60-125">Required</span><span class="sxs-lookup"><span data-stu-id="cbb60-125">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cbb60-126">type</span><span class="sxs-lookup"><span data-stu-id="cbb60-126">type</span></span> | <span data-ttu-id="cbb60-127">The type property must be set to: **Sybase**</span><span class="sxs-lookup"><span data-stu-id="cbb60-127">The type property must be set to: **Sybase**</span></span> | <span data-ttu-id="cbb60-128">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-128">Yes</span></span> |
| <span data-ttu-id="cbb60-129">server</span><span class="sxs-lookup"><span data-stu-id="cbb60-129">server</span></span> | <span data-ttu-id="cbb60-130">Name of the Sybase server.</span><span class="sxs-lookup"><span data-stu-id="cbb60-130">Name of the Sybase server.</span></span> |<span data-ttu-id="cbb60-131">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-131">Yes</span></span> |
| <span data-ttu-id="cbb60-132">database</span><span class="sxs-lookup"><span data-stu-id="cbb60-132">database</span></span> | <span data-ttu-id="cbb60-133">Name of the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="cbb60-133">Name of the Sybase database.</span></span> |<span data-ttu-id="cbb60-134">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-134">Yes</span></span> |
| <span data-ttu-id="cbb60-135">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cbb60-135">authenticationType</span></span> | <span data-ttu-id="cbb60-136">Type of authentication used to connect to the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="cbb60-136">Type of authentication used to connect to the Sybase database.</span></span><br/><span data-ttu-id="cbb60-137">Allowed values are: **Basic**, and **Windows**.</span><span class="sxs-lookup"><span data-stu-id="cbb60-137">Allowed values are: **Basic**, and **Windows**.</span></span> |<span data-ttu-id="cbb60-138">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-138">Yes</span></span> |
| <span data-ttu-id="cbb60-139">username</span><span class="sxs-lookup"><span data-stu-id="cbb60-139">username</span></span> | <span data-ttu-id="cbb60-140">Specify user name to connect to the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="cbb60-140">Specify user name to connect to the Sybase database.</span></span> |<span data-ttu-id="cbb60-141">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-141">Yes</span></span> |
| <span data-ttu-id="cbb60-142">password</span><span class="sxs-lookup"><span data-stu-id="cbb60-142">password</span></span> | <span data-ttu-id="cbb60-143">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="cbb60-143">Specify password for the user account you specified for the username.</span></span> <span data-ttu-id="cbb60-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cbb60-144">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="cbb60-145">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-145">Yes</span></span> |
| <span data-ttu-id="cbb60-146">connectVia</span><span class="sxs-lookup"><span data-stu-id="cbb60-146">connectVia</span></span> | <span data-ttu-id="cbb60-147">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="cbb60-147">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="cbb60-148">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="cbb60-148">A Self-hosted Integration Runtime is required as mentioned in [Prerequisites](#prerequisites).</span></span> |<span data-ttu-id="cbb60-149">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-149">Yes</span></span> |

<span data-ttu-id="cbb60-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="cbb60-150">**Example:**</span></span>

```json
{
    "name": "SybaseLinkedService",
    "properties": {
        "type": "Sybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
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

## <a name="dataset-properties"></a><span data-ttu-id="cbb60-151">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="cbb60-151">Dataset properties</span></span>

<span data-ttu-id="cbb60-152">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="cbb60-152">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="cbb60-153">This section provides a list of properties supported by Sybase dataset.</span><span class="sxs-lookup"><span data-stu-id="cbb60-153">This section provides a list of properties supported by Sybase dataset.</span></span>

<span data-ttu-id="cbb60-154">To copy data from Sybase, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="cbb60-154">To copy data from Sybase, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="cbb60-155">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="cbb60-155">The following properties are supported:</span></span>

| <span data-ttu-id="cbb60-156">Property</span><span class="sxs-lookup"><span data-stu-id="cbb60-156">Property</span></span> | <span data-ttu-id="cbb60-157">Description</span><span class="sxs-lookup"><span data-stu-id="cbb60-157">Description</span></span> | <span data-ttu-id="cbb60-158">Required</span><span class="sxs-lookup"><span data-stu-id="cbb60-158">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cbb60-159">type</span><span class="sxs-lookup"><span data-stu-id="cbb60-159">type</span></span> | <span data-ttu-id="cbb60-160">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="cbb60-160">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="cbb60-161">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-161">Yes</span></span> |
| <span data-ttu-id="cbb60-162">tableName</span><span class="sxs-lookup"><span data-stu-id="cbb60-162">tableName</span></span> | <span data-ttu-id="cbb60-163">Name of the table in the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="cbb60-163">Name of the table in the Sybase database.</span></span> | <span data-ttu-id="cbb60-164">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="cbb60-164">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="cbb60-165">**Example**</span><span class="sxs-lookup"><span data-stu-id="cbb60-165">**Example**</span></span>

```json
{
    "name": "SybaseDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<Sybase linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="cbb60-166">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="cbb60-166">Copy activity properties</span></span>

<span data-ttu-id="cbb60-167">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="cbb60-167">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="cbb60-168">This section provides a list of properties supported by Sybase source.</span><span class="sxs-lookup"><span data-stu-id="cbb60-168">This section provides a list of properties supported by Sybase source.</span></span>

### <a name="sybase-as-source"></a><span data-ttu-id="cbb60-169">Sybase as source</span><span class="sxs-lookup"><span data-stu-id="cbb60-169">Sybase as source</span></span>

<span data-ttu-id="cbb60-170">To copy data from Sybase, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="cbb60-170">To copy data from Sybase, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="cbb60-171">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="cbb60-171">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="cbb60-172">Property</span><span class="sxs-lookup"><span data-stu-id="cbb60-172">Property</span></span> | <span data-ttu-id="cbb60-173">Description</span><span class="sxs-lookup"><span data-stu-id="cbb60-173">Description</span></span> | <span data-ttu-id="cbb60-174">Required</span><span class="sxs-lookup"><span data-stu-id="cbb60-174">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="cbb60-175">type</span><span class="sxs-lookup"><span data-stu-id="cbb60-175">type</span></span> | <span data-ttu-id="cbb60-176">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="cbb60-176">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="cbb60-177">Yes</span><span class="sxs-lookup"><span data-stu-id="cbb60-177">Yes</span></span> |
| <span data-ttu-id="cbb60-178">query</span><span class="sxs-lookup"><span data-stu-id="cbb60-178">query</span></span> | <span data-ttu-id="cbb60-179">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="cbb60-179">Use the custom SQL query to read data.</span></span> <span data-ttu-id="cbb60-180">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="cbb60-180">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="cbb60-181">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="cbb60-181">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="cbb60-182">**Example:**</span><span class="sxs-lookup"><span data-stu-id="cbb60-182">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromSybase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Sybase input dataset name>",
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

## <a name="data-type-mapping-for-sybase"></a><span data-ttu-id="cbb60-183">Data type mapping for Sybase</span><span class="sxs-lookup"><span data-stu-id="cbb60-183">Data type mapping for Sybase</span></span>

<span data-ttu-id="cbb60-184">When copying data from Sybase, the following mappings are used from Sybase data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="cbb60-184">When copying data from Sybase, the following mappings are used from Sybase data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="cbb60-185">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="cbb60-185">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

<span data-ttu-id="cbb60-186">Sybase supports T-SQL types.</span><span class="sxs-lookup"><span data-stu-id="cbb60-186">Sybase supports T-SQL types.</span></span> <span data-ttu-id="cbb60-187">For a mapping table from SQL types to Azure Data Factory interim data types, see [Azure SQL Database Connector - data type mapping](connector-azure-sql-database.md#data-type-mapping-for-azure-sql-database) section.</span><span class="sxs-lookup"><span data-stu-id="cbb60-187">For a mapping table from SQL types to Azure Data Factory interim data types, see [Azure SQL Database Connector - data type mapping](connector-azure-sql-database.md#data-type-mapping-for-azure-sql-database) section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cbb60-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbb60-188">Next steps</span></span>
<span data-ttu-id="cbb60-189">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="cbb60-189">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
