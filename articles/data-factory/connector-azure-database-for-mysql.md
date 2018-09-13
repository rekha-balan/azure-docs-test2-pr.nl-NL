---
title: Copy data from Azure Database for MySQL using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Azure Database for MySQL to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 04/28/2018
ms.author: jingwang
ms.openlocfilehash: e254c9b18d86debad7ba914a0a4d41369795bc58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867322"
---
# <a name="copy-data-from-azure-database-for-mysql-using-azure-data-factory"></a><span data-ttu-id="a2200-103">Copy data from Azure Database for MySQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a2200-103">Copy data from Azure Database for MySQL using Azure Data Factory</span></span>

<span data-ttu-id="a2200-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2200-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Azure Database for MySQL.</span></span> <span data-ttu-id="a2200-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="a2200-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="a2200-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="a2200-106">Supported capabilities</span></span>

<span data-ttu-id="a2200-107">You can copy data from Azure Database for MySQL to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="a2200-107">You can copy data from Azure Database for MySQL to any supported sink data store.</span></span> <span data-ttu-id="a2200-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="a2200-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="a2200-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="a2200-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a2200-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="a2200-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="a2200-111">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Database for MySQL connector.</span><span class="sxs-lookup"><span data-stu-id="a2200-111">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Database for MySQL connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a2200-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="a2200-112">Linked service properties</span></span>

<span data-ttu-id="a2200-113">The following properties are supported for Azure Database for MySQL linked service:</span><span class="sxs-lookup"><span data-stu-id="a2200-113">The following properties are supported for Azure Database for MySQL linked service:</span></span>

| <span data-ttu-id="a2200-114">Property</span><span class="sxs-lookup"><span data-stu-id="a2200-114">Property</span></span> | <span data-ttu-id="a2200-115">Description</span><span class="sxs-lookup"><span data-stu-id="a2200-115">Description</span></span> | <span data-ttu-id="a2200-116">Required</span><span class="sxs-lookup"><span data-stu-id="a2200-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a2200-117">type</span><span class="sxs-lookup"><span data-stu-id="a2200-117">type</span></span> | <span data-ttu-id="a2200-118">The type property must be set to: **AzureMySql**</span><span class="sxs-lookup"><span data-stu-id="a2200-118">The type property must be set to: **AzureMySql**</span></span> | <span data-ttu-id="a2200-119">Yes</span><span class="sxs-lookup"><span data-stu-id="a2200-119">Yes</span></span> |
| <span data-ttu-id="a2200-120">connectionString</span><span class="sxs-lookup"><span data-stu-id="a2200-120">connectionString</span></span> | <span data-ttu-id="a2200-121">Specify information needed to connect to the Azure Database for MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="a2200-121">Specify information needed to connect to the Azure Database for MySQL instance.</span></span> <span data-ttu-id="a2200-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="a2200-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="a2200-123">Yes</span><span class="sxs-lookup"><span data-stu-id="a2200-123">Yes</span></span> |
| <span data-ttu-id="a2200-124">connectVia</span><span class="sxs-lookup"><span data-stu-id="a2200-124">connectVia</span></span> | <span data-ttu-id="a2200-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="a2200-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="a2200-126">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="a2200-126">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="a2200-127">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="a2200-127">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="a2200-128">No</span><span class="sxs-lookup"><span data-stu-id="a2200-128">No</span></span> |

<span data-ttu-id="a2200-129">A typical connection string is `Server=<server>.mysql.database.azure.com;Port=<port>;Database=<database>;UID=<username>;PWD=<password>`.</span><span class="sxs-lookup"><span data-stu-id="a2200-129">A typical connection string is `Server=<server>.mysql.database.azure.com;Port=<port>;Database=<database>;UID=<username>;PWD=<password>`.</span></span> <span data-ttu-id="a2200-130">More properties you can set per your case:</span><span class="sxs-lookup"><span data-stu-id="a2200-130">More properties you can set per your case:</span></span>

| <span data-ttu-id="a2200-131">Property</span><span class="sxs-lookup"><span data-stu-id="a2200-131">Property</span></span> | <span data-ttu-id="a2200-132">Description</span><span class="sxs-lookup"><span data-stu-id="a2200-132">Description</span></span> | <span data-ttu-id="a2200-133">Options</span><span class="sxs-lookup"><span data-stu-id="a2200-133">Options</span></span> | <span data-ttu-id="a2200-134">Required</span><span class="sxs-lookup"><span data-stu-id="a2200-134">Required</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="a2200-135">SSLMode</span><span class="sxs-lookup"><span data-stu-id="a2200-135">SSLMode</span></span> | <span data-ttu-id="a2200-136">This option specifies whether the driver uses SSL encryption and verification when connecting to MySQL.</span><span class="sxs-lookup"><span data-stu-id="a2200-136">This option specifies whether the driver uses SSL encryption and verification when connecting to MySQL.</span></span> <span data-ttu-id="a2200-137">E.g.</span><span class="sxs-lookup"><span data-stu-id="a2200-137">E.g.</span></span> `SSLMode=<0/1/2/3/4>`| <span data-ttu-id="a2200-138">DISABLED (0) / PREFERRED (1) **(Default)** / REQUIRED (2) / VERIFY_CA (3) / VERIFY_IDENTITY (4)</span><span class="sxs-lookup"><span data-stu-id="a2200-138">DISABLED (0) / PREFERRED (1) **(Default)** / REQUIRED (2) / VERIFY_CA (3) / VERIFY_IDENTITY (4)</span></span> | <span data-ttu-id="a2200-139">No</span><span class="sxs-lookup"><span data-stu-id="a2200-139">No</span></span> |
| <span data-ttu-id="a2200-140">UseSystemTrustStore</span><span class="sxs-lookup"><span data-stu-id="a2200-140">UseSystemTrustStore</span></span> | <span data-ttu-id="a2200-141">This option specifies whether to use a CA certificate from the system trust store, or from a specified PEM file.</span><span class="sxs-lookup"><span data-stu-id="a2200-141">This option specifies whether to use a CA certificate from the system trust store, or from a specified PEM file.</span></span> <span data-ttu-id="a2200-142">E.g.</span><span class="sxs-lookup"><span data-stu-id="a2200-142">E.g.</span></span> `UseSystemTrustStore=<0/1>;`| <span data-ttu-id="a2200-143">Enabled (1) / Disabled (0) **(Default)**</span><span class="sxs-lookup"><span data-stu-id="a2200-143">Enabled (1) / Disabled (0) **(Default)**</span></span> | <span data-ttu-id="a2200-144">No</span><span class="sxs-lookup"><span data-stu-id="a2200-144">No</span></span> |

<span data-ttu-id="a2200-145">**Example:**</span><span class="sxs-lookup"><span data-stu-id="a2200-145">**Example:**</span></span>

```json
{
    "name": "AzureDatabaseForMySQLLinkedService",
    "properties": {
        "type": "AzureMySql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>.mysql.database.azure.com;Port=<port>;Database=<database>;UID=<username>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a2200-146">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="a2200-146">Dataset properties</span></span>

<span data-ttu-id="a2200-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2200-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="a2200-148">This section provides a list of properties supported by Azure Database for MySQL dataset.</span><span class="sxs-lookup"><span data-stu-id="a2200-148">This section provides a list of properties supported by Azure Database for MySQL dataset.</span></span>

<span data-ttu-id="a2200-149">To copy data from Azure Database for MySQL, set the type property of the dataset to **AzureMySqlTable**.</span><span class="sxs-lookup"><span data-stu-id="a2200-149">To copy data from Azure Database for MySQL, set the type property of the dataset to **AzureMySqlTable**.</span></span> <span data-ttu-id="a2200-150">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="a2200-150">The following properties are supported:</span></span>

| <span data-ttu-id="a2200-151">Property</span><span class="sxs-lookup"><span data-stu-id="a2200-151">Property</span></span> | <span data-ttu-id="a2200-152">Description</span><span class="sxs-lookup"><span data-stu-id="a2200-152">Description</span></span> | <span data-ttu-id="a2200-153">Required</span><span class="sxs-lookup"><span data-stu-id="a2200-153">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a2200-154">type</span><span class="sxs-lookup"><span data-stu-id="a2200-154">type</span></span> | <span data-ttu-id="a2200-155">The type property of the dataset must be set to: **AzureMySqlTable**</span><span class="sxs-lookup"><span data-stu-id="a2200-155">The type property of the dataset must be set to: **AzureMySqlTable**</span></span> | <span data-ttu-id="a2200-156">Yes</span><span class="sxs-lookup"><span data-stu-id="a2200-156">Yes</span></span> |
| <span data-ttu-id="a2200-157">tableName</span><span class="sxs-lookup"><span data-stu-id="a2200-157">tableName</span></span> | <span data-ttu-id="a2200-158">Name of the table in the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="a2200-158">Name of the table in the MySQL database.</span></span> | <span data-ttu-id="a2200-159">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="a2200-159">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="a2200-160">**Example**</span><span class="sxs-lookup"><span data-stu-id="a2200-160">**Example**</span></span>

```json
{
    "name": "AzureMySQLDataset",
    "properties": {
        "type": "AzureMySqlTable",
        "linkedServiceName": {
            "referenceName": "<Azure MySQL linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "<table name>"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="a2200-161">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="a2200-161">Copy activity properties</span></span>

<span data-ttu-id="a2200-162">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="a2200-162">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="a2200-163">This section provides a list of properties supported by Azure Database for MySQL source.</span><span class="sxs-lookup"><span data-stu-id="a2200-163">This section provides a list of properties supported by Azure Database for MySQL source.</span></span>

### <a name="azure-database-for-mysql-as-source"></a><span data-ttu-id="a2200-164">Azure Database for MySQL as source</span><span class="sxs-lookup"><span data-stu-id="a2200-164">Azure Database for MySQL as source</span></span>

<span data-ttu-id="a2200-165">To copy data from Azure Database for MySQL, set the source type in the copy activity to **AzureMySqlSource**.</span><span class="sxs-lookup"><span data-stu-id="a2200-165">To copy data from Azure Database for MySQL, set the source type in the copy activity to **AzureMySqlSource**.</span></span> <span data-ttu-id="a2200-166">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="a2200-166">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="a2200-167">Property</span><span class="sxs-lookup"><span data-stu-id="a2200-167">Property</span></span> | <span data-ttu-id="a2200-168">Description</span><span class="sxs-lookup"><span data-stu-id="a2200-168">Description</span></span> | <span data-ttu-id="a2200-169">Required</span><span class="sxs-lookup"><span data-stu-id="a2200-169">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a2200-170">type</span><span class="sxs-lookup"><span data-stu-id="a2200-170">type</span></span> | <span data-ttu-id="a2200-171">The type property of the copy activity source must be set to: **AzureMySqlSource**</span><span class="sxs-lookup"><span data-stu-id="a2200-171">The type property of the copy activity source must be set to: **AzureMySqlSource**</span></span> | <span data-ttu-id="a2200-172">Yes</span><span class="sxs-lookup"><span data-stu-id="a2200-172">Yes</span></span> |
| <span data-ttu-id="a2200-173">query</span><span class="sxs-lookup"><span data-stu-id="a2200-173">query</span></span> | <span data-ttu-id="a2200-174">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="a2200-174">Use the custom SQL query to read data.</span></span> <span data-ttu-id="a2200-175">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="a2200-175">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="a2200-176">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="a2200-176">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="a2200-177">**Example:**</span><span class="sxs-lookup"><span data-stu-id="a2200-177">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzureDatabaseForMySQL",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Azure MySQL input dataset name>",
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
                "type": "AzureMySqlSource",
                "query": "<custom query e.g. SELECT * FROM MyTable>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-azure-database-for-mysql"></a><span data-ttu-id="a2200-178">Data type mapping for Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a2200-178">Data type mapping for Azure Database for MySQL</span></span>

<span data-ttu-id="a2200-179">When copying data from Azure Database for MySQL, the following mappings are used from MySQL data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="a2200-179">When copying data from Azure Database for MySQL, the following mappings are used from MySQL data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="a2200-180">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="a2200-180">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="a2200-181">Azure Database for MySQL data type</span><span class="sxs-lookup"><span data-stu-id="a2200-181">Azure Database for MySQL data type</span></span> | <span data-ttu-id="a2200-182">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="a2200-182">Data factory interim data type</span></span> |
|:--- |:--- |
| `bigint` |`Int64` |
| `bigint unsigned` |`Decimal` |
| `bit` |`Boolean` |
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
| `year` |`Int32` |


## <a name="next-steps"></a><span data-ttu-id="a2200-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2200-183">Next steps</span></span>
<span data-ttu-id="a2200-184">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a2200-184">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
