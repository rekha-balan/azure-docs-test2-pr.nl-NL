---
title: Copy data from MySQL using Azure Data Factory | Microsoft Docs
description: Learn about MySQL connector in Azure Data Factory that lets you copy data from a MySQL database to a data store supported as a sink.
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
ms.date: 06/23/2018
ms.author: jingwang
ms.openlocfilehash: bb3179f1db077aacc7e36acf16486ee77a7f36e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869359"
---
# <a name="copy-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="4c863-103">Copy data from MySQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4c863-103">Copy data from MySQL using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-mysql-connector.md)
> * [Current version](connector-mysql.md)

<span data-ttu-id="4c863-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4c863-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a MySQL database.</span></span> <span data-ttu-id="4c863-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="4c863-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="4c863-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="4c863-108">Supported capabilities</span></span>

<span data-ttu-id="4c863-109">You can copy data from MySQL database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="4c863-109">You can copy data from MySQL database to any supported sink data store.</span></span> <span data-ttu-id="4c863-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="4c863-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="4c863-111">Specifically, this MySQL connector supports MySQL **version 5.1 and above**.</span><span class="sxs-lookup"><span data-stu-id="4c863-111">Specifically, this MySQL connector supports MySQL **version 5.1 and above**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c863-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4c863-112">Prerequisites</span></span>

<span data-ttu-id="4c863-113">If your MySQL database is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="4c863-113">If your MySQL database is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="4c863-114">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span><span class="sxs-lookup"><span data-stu-id="4c863-114">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span></span> <span data-ttu-id="4c863-115">The Integration Runtime provides a built-in MySQL driver starting from version 3.7, therefore you don't need to manually install any driver.</span><span class="sxs-lookup"><span data-stu-id="4c863-115">The Integration Runtime provides a built-in MySQL driver starting from version 3.7, therefore you don't need to manually install any driver.</span></span>

<span data-ttu-id="4c863-116">For Self-hosted IR version lower than 3.7, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) version between 6.6.5 and 6.10.7 on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="4c863-116">For Self-hosted IR version lower than 3.7, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) version between 6.6.5 and 6.10.7 on the Integration Runtime machine.</span></span> <span data-ttu-id="4c863-117">This 32 bit driver is compatible with 64 bit IR.</span><span class="sxs-lookup"><span data-stu-id="4c863-117">This 32 bit driver is compatible with 64 bit IR.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4c863-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="4c863-118">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="4c863-119">The following sections provide details about properties that are used to define Data Factory entities specific to MySQL connector.</span><span class="sxs-lookup"><span data-stu-id="4c863-119">The following sections provide details about properties that are used to define Data Factory entities specific to MySQL connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4c863-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="4c863-120">Linked service properties</span></span>

<span data-ttu-id="4c863-121">The following properties are supported for MySQL linked service:</span><span class="sxs-lookup"><span data-stu-id="4c863-121">The following properties are supported for MySQL linked service:</span></span>

| <span data-ttu-id="4c863-122">Property</span><span class="sxs-lookup"><span data-stu-id="4c863-122">Property</span></span> | <span data-ttu-id="4c863-123">Description</span><span class="sxs-lookup"><span data-stu-id="4c863-123">Description</span></span> | <span data-ttu-id="4c863-124">Required</span><span class="sxs-lookup"><span data-stu-id="4c863-124">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4c863-125">type</span><span class="sxs-lookup"><span data-stu-id="4c863-125">type</span></span> | <span data-ttu-id="4c863-126">The type property must be set to: **MySql**</span><span class="sxs-lookup"><span data-stu-id="4c863-126">The type property must be set to: **MySql**</span></span> | <span data-ttu-id="4c863-127">Yes</span><span class="sxs-lookup"><span data-stu-id="4c863-127">Yes</span></span> |
| <span data-ttu-id="4c863-128">connectionString</span><span class="sxs-lookup"><span data-stu-id="4c863-128">connectionString</span></span> | <span data-ttu-id="4c863-129">Specify information needed to connect to the Azure Database for MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="4c863-129">Specify information needed to connect to the Azure Database for MySQL instance.</span></span> <span data-ttu-id="4c863-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="4c863-130">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="4c863-131">Yes</span><span class="sxs-lookup"><span data-stu-id="4c863-131">Yes</span></span> |
| <span data-ttu-id="4c863-132">connectVia</span><span class="sxs-lookup"><span data-stu-id="4c863-132">connectVia</span></span> | <span data-ttu-id="4c863-133">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="4c863-133">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="4c863-134">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="4c863-134">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="4c863-135">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="4c863-135">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="4c863-136">No</span><span class="sxs-lookup"><span data-stu-id="4c863-136">No</span></span> |

<span data-ttu-id="4c863-137">A typical connection string is `Server=<server>;Port=<port>;Database=<database>;UID=<username>;PWD=<password>`.</span><span class="sxs-lookup"><span data-stu-id="4c863-137">A typical connection string is `Server=<server>;Port=<port>;Database=<database>;UID=<username>;PWD=<password>`.</span></span> <span data-ttu-id="4c863-138">More properties you can set per your case:</span><span class="sxs-lookup"><span data-stu-id="4c863-138">More properties you can set per your case:</span></span>

| <span data-ttu-id="4c863-139">Property</span><span class="sxs-lookup"><span data-stu-id="4c863-139">Property</span></span> | <span data-ttu-id="4c863-140">Description</span><span class="sxs-lookup"><span data-stu-id="4c863-140">Description</span></span> | <span data-ttu-id="4c863-141">Options</span><span class="sxs-lookup"><span data-stu-id="4c863-141">Options</span></span> | <span data-ttu-id="4c863-142">Required</span><span class="sxs-lookup"><span data-stu-id="4c863-142">Required</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="4c863-143">SSLMode</span><span class="sxs-lookup"><span data-stu-id="4c863-143">SSLMode</span></span> | <span data-ttu-id="4c863-144">This option specifies whether the driver uses SSL encryption and verification when connecting to MySQL.</span><span class="sxs-lookup"><span data-stu-id="4c863-144">This option specifies whether the driver uses SSL encryption and verification when connecting to MySQL.</span></span> <span data-ttu-id="4c863-145">E.g.</span><span class="sxs-lookup"><span data-stu-id="4c863-145">E.g.</span></span> `SSLMode=<0/1/2/3/4>`| <span data-ttu-id="4c863-146">DISABLED (0) / PREFERRED (1) **(Default)** / REQUIRED (2) / VERIFY_CA (3) / VERIFY_IDENTITY (4)</span><span class="sxs-lookup"><span data-stu-id="4c863-146">DISABLED (0) / PREFERRED (1) **(Default)** / REQUIRED (2) / VERIFY_CA (3) / VERIFY_IDENTITY (4)</span></span> | <span data-ttu-id="4c863-147">No</span><span class="sxs-lookup"><span data-stu-id="4c863-147">No</span></span> |
| <span data-ttu-id="4c863-148">UseSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="4c863-148">UseSystemTrustStore</span></span> | <span data-ttu-id="4c863-149">This option specifies whether to use a CA certificate from the system trust store, or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="4c863-149">This option specifies whether to use a CA certificate from the system trust store, or from a specified PEM file.</span></span> <span data-ttu-id="4c863-150">E.g.</span><span class="sxs-lookup"><span data-stu-id="4c863-150">E.g.</span></span> `UseSystemTrustStore=<0/1>;`| <span data-ttu-id="4c863-151">Enabled (1) / Disabled (0) **(Default)**</span><span class="sxs-lookup"><span data-stu-id="4c863-151">Enabled (1) / Disabled (0) **(Default)**</span></span> | <span data-ttu-id="4c863-152">No</span><span class="sxs-lookup"><span data-stu-id="4c863-152">No</span></span> |

<span data-ttu-id="4c863-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="4c863-153">**Example:**</span></span>

```json
{
    "name": "MySQLLinkedService",
    "properties": {
        "type": "MySql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>;Port=<port>;Database=<database>;UID=<username>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="4c863-154">If you were using MySQL linked service with the following payload, it is still supported as-is, while you are suggested to use the new one going forward.</span><span class="sxs-lookup"><span data-stu-id="4c863-154">If you were using MySQL linked service with the following payload, it is still supported as-is, while you are suggested to use the new one going forward.</span></span>

<span data-ttu-id="4c863-155">**Previous payload:**</span><span class="sxs-lookup"><span data-stu-id="4c863-155">**Previous payload:**</span></span>

```json
{
    "name": "MySQLLinkedService",
    "properties": {
        "type": "MySql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
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

## <a name="dataset-properties"></a><span data-ttu-id="4c863-156">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="4c863-156">Dataset properties</span></span>

<span data-ttu-id="4c863-157">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="4c863-157">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="4c863-158">This section provides a list of properties supported by MySQL dataset.</span><span class="sxs-lookup"><span data-stu-id="4c863-158">This section provides a list of properties supported by MySQL dataset.</span></span>

<span data-ttu-id="4c863-159">To copy data from MySQL, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="4c863-159">To copy data from MySQL, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="4c863-160">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="4c863-160">The following properties are supported:</span></span>

| <span data-ttu-id="4c863-161">Property</span><span class="sxs-lookup"><span data-stu-id="4c863-161">Property</span></span> | <span data-ttu-id="4c863-162">Description</span><span class="sxs-lookup"><span data-stu-id="4c863-162">Description</span></span> | <span data-ttu-id="4c863-163">Required</span><span class="sxs-lookup"><span data-stu-id="4c863-163">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4c863-164">type</span><span class="sxs-lookup"><span data-stu-id="4c863-164">type</span></span> | <span data-ttu-id="4c863-165">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="4c863-165">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="4c863-166">Yes</span><span class="sxs-lookup"><span data-stu-id="4c863-166">Yes</span></span> |
| <span data-ttu-id="4c863-167">tableName</span><span class="sxs-lookup"><span data-stu-id="4c863-167">tableName</span></span> | <span data-ttu-id="4c863-168">Name of the table in the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4c863-168">Name of the table in the MySQL database.</span></span> | <span data-ttu-id="4c863-169">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="4c863-169">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="4c863-170">**Example**</span><span class="sxs-lookup"><span data-stu-id="4c863-170">**Example**</span></span>

```json
{
    "name": "MySQLDataset",
    "properties":
    {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<MySQL linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="4c863-171">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="4c863-171">Copy activity properties</span></span>

<span data-ttu-id="4c863-172">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="4c863-172">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="4c863-173">This section provides a list of properties supported by MySQL source.</span><span class="sxs-lookup"><span data-stu-id="4c863-173">This section provides a list of properties supported by MySQL source.</span></span>

### <a name="mysql-as-source"></a><span data-ttu-id="4c863-174">MySQL as source</span><span class="sxs-lookup"><span data-stu-id="4c863-174">MySQL as source</span></span>

<span data-ttu-id="4c863-175">To copy data from MySQL, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="4c863-175">To copy data from MySQL, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="4c863-176">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="4c863-176">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="4c863-177">Property</span><span class="sxs-lookup"><span data-stu-id="4c863-177">Property</span></span> | <span data-ttu-id="4c863-178">Description</span><span class="sxs-lookup"><span data-stu-id="4c863-178">Description</span></span> | <span data-ttu-id="4c863-179">Required</span><span class="sxs-lookup"><span data-stu-id="4c863-179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4c863-180">type</span><span class="sxs-lookup"><span data-stu-id="4c863-180">type</span></span> | <span data-ttu-id="4c863-181">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="4c863-181">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="4c863-182">Yes</span><span class="sxs-lookup"><span data-stu-id="4c863-182">Yes</span></span> |
| <span data-ttu-id="4c863-183">query</span><span class="sxs-lookup"><span data-stu-id="4c863-183">query</span></span> | <span data-ttu-id="4c863-184">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="4c863-184">Use the custom SQL query to read data.</span></span> <span data-ttu-id="4c863-185">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="4c863-185">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="4c863-186">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="4c863-186">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="4c863-187">**Example:**</span><span class="sxs-lookup"><span data-stu-id="4c863-187">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromMySQL",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MySQL input dataset name>",
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

## <a name="data-type-mapping-for-mysql"></a><span data-ttu-id="4c863-188">Data type mapping for MySQL</span><span class="sxs-lookup"><span data-stu-id="4c863-188">Data type mapping for MySQL</span></span>

<span data-ttu-id="4c863-189">When copying data from MySQL, the following mappings are used from MySQL data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="4c863-189">When copying data from MySQL, the following mappings are used from MySQL data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="4c863-190">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="4c863-190">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="4c863-191">MySQL data type</span><span class="sxs-lookup"><span data-stu-id="4c863-191">MySQL data type</span></span> | <span data-ttu-id="4c863-192">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="4c863-192">Data factory interim data type</span></span> |
|:--- |:--- |
| `bigint` |`Int64` |
| `bigint unsigned` |`Decimal` |
| `bit(1)` |`Boolean` |
| `bit(M), M>1`|`Byte[]`|
| `blob` |`Byte[]` |
| `bool` |`Int16` |
| `char` |`String` |
| `date` |`Datetime` |
| `datetime` |`Datetime` |
| `decimal` |`Decimal, String` |
| `double` |`Double` |
| `double precision` |`Double` |
| `enum` |`String` |
| `float` |`Single` |
| `int` |`Int32` |
| `int unsigned` |`Int64`|
| `integer` |`Int32` |
| `integer unsigned` |`Int64` |
| `long varbinary` |`Byte[]` |
| `long varchar` |`String` |
| `longblob` |`Byte[]` |
| `longtext` |`String` |
| `mediumblob` |`Byte[]` |
| `mediumint` |`Int32` |
| `mediumint unsigned` |`Int64` |
| `mediumtext` |`String` |
| `numeric` |`Decimal` |
| `real` |`Double` |
| `set` |`String` |
| `smallint` |`Int16` |
| `smallint unsigned` |`Int32` |
| `text` |`String` |
| `time` |`TimeSpan` |
| `timestamp` |`Datetime` |
| `tinyblob` |`Byte[]` |
| `tinyint` |`Int16` |
| `tinyint unsigned` |`Int16` |
| `tinytext` |`String` |
| `varchar` |`String` |
| `year` |`Int` |


## <a name="next-steps"></a><span data-ttu-id="4c863-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c863-193">Next steps</span></span>
<span data-ttu-id="4c863-194">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4c863-194">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
