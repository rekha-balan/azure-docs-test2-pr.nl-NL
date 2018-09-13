---
title: Copy data from Azure Database for PostgreSQL using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Azure Database for PostgreSQL to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 1c1d9f7a4b64ea1e952b3edd9011f5dc197543d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969287"
---
# <a name="copy-data-from-azure-database-for-postgresql-using-azure-data-factory"></a><span data-ttu-id="715e7-103">Copy data from Azure Database for PostgreSQL using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="715e7-103">Copy data from Azure Database for PostgreSQL using Azure Data Factory</span></span> 

<span data-ttu-id="715e7-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="715e7-104">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from Azure Database for PostgreSQL.</span></span> <span data-ttu-id="715e7-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="715e7-105">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="715e7-106">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="715e7-106">Supported capabilities</span></span>

<span data-ttu-id="715e7-107">You can copy data from Azure Database for PostgreSQL to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="715e7-107">You can copy data from Azure Database for PostgreSQL to any supported sink data store.</span></span> <span data-ttu-id="715e7-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="715e7-108">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="715e7-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span><span class="sxs-lookup"><span data-stu-id="715e7-109">Azure Data Factory provides a built-in driver to enable connectivity, therefore you don't need to manually install any driver using this connector.</span></span>

## <a name="getting-started"></a><span data-ttu-id="715e7-110">Getting started</span><span class="sxs-lookup"><span data-stu-id="715e7-110">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="715e7-111">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Database for PostgreSQL connector.</span><span class="sxs-lookup"><span data-stu-id="715e7-111">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Database for PostgreSQL connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="715e7-112">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="715e7-112">Linked service properties</span></span>

<span data-ttu-id="715e7-113">The following properties are supported for Azure Database for PostgreSQL linked service:</span><span class="sxs-lookup"><span data-stu-id="715e7-113">The following properties are supported for Azure Database for PostgreSQL linked service:</span></span>

| <span data-ttu-id="715e7-114">Property</span><span class="sxs-lookup"><span data-stu-id="715e7-114">Property</span></span> | <span data-ttu-id="715e7-115">Description</span><span class="sxs-lookup"><span data-stu-id="715e7-115">Description</span></span> | <span data-ttu-id="715e7-116">Required</span><span class="sxs-lookup"><span data-stu-id="715e7-116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="715e7-117">type</span><span class="sxs-lookup"><span data-stu-id="715e7-117">type</span></span> | <span data-ttu-id="715e7-118">The type property must be set to: **AzurePostgreSql**</span><span class="sxs-lookup"><span data-stu-id="715e7-118">The type property must be set to: **AzurePostgreSql**</span></span> | <span data-ttu-id="715e7-119">Yes</span><span class="sxs-lookup"><span data-stu-id="715e7-119">Yes</span></span> |
| <span data-ttu-id="715e7-120">connectionString</span><span class="sxs-lookup"><span data-stu-id="715e7-120">connectionString</span></span> | <span data-ttu-id="715e7-121">An ODBC connection string to connect to Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="715e7-121">An ODBC connection string to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="715e7-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="715e7-122">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="715e7-123">Yes</span><span class="sxs-lookup"><span data-stu-id="715e7-123">Yes</span></span> |
| <span data-ttu-id="715e7-124">connectVia</span><span class="sxs-lookup"><span data-stu-id="715e7-124">connectVia</span></span> | <span data-ttu-id="715e7-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="715e7-125">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="715e7-126">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="715e7-126">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="715e7-127">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="715e7-127">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="715e7-128">No</span><span class="sxs-lookup"><span data-stu-id="715e7-128">No</span></span> |

<span data-ttu-id="715e7-129">A typical connection string is `Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>;Password=<Password>`.</span><span class="sxs-lookup"><span data-stu-id="715e7-129">A typical connection string is `Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>;Password=<Password>`.</span></span> <span data-ttu-id="715e7-130">More properties you can set per your case:</span><span class="sxs-lookup"><span data-stu-id="715e7-130">More properties you can set per your case:</span></span>

| <span data-ttu-id="715e7-131">Property</span><span class="sxs-lookup"><span data-stu-id="715e7-131">Property</span></span> | <span data-ttu-id="715e7-132">Description</span><span class="sxs-lookup"><span data-stu-id="715e7-132">Description</span></span> | <span data-ttu-id="715e7-133">Options</span><span class="sxs-lookup"><span data-stu-id="715e7-133">Options</span></span> | <span data-ttu-id="715e7-134">Required</span><span class="sxs-lookup"><span data-stu-id="715e7-134">Required</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="715e7-135">EncryptionMethod (EM)</span><span class="sxs-lookup"><span data-stu-id="715e7-135">EncryptionMethod (EM)</span></span>| <span data-ttu-id="715e7-136">The method the driver uses to encrypt data sent between the driver and the database server.</span><span class="sxs-lookup"><span data-stu-id="715e7-136">The method the driver uses to encrypt data sent between the driver and the database server.</span></span> <span data-ttu-id="715e7-137">E.g.</span><span class="sxs-lookup"><span data-stu-id="715e7-137">E.g.</span></span> `ValidateServerCertificate=<0/1/6>;`| <span data-ttu-id="715e7-138">0 (No Encryption) **(Default)** / 1 (SSL) / 6 (RequestSSL)</span><span class="sxs-lookup"><span data-stu-id="715e7-138">0 (No Encryption) **(Default)** / 1 (SSL) / 6 (RequestSSL)</span></span> | <span data-ttu-id="715e7-139">No</span><span class="sxs-lookup"><span data-stu-id="715e7-139">No</span></span> |
| <span data-ttu-id="715e7-140">ValidateServerCertificate (VSC)</span><span class="sxs-lookup"><span data-stu-id="715e7-140">ValidateServerCertificate (VSC)</span></span> | <span data-ttu-id="715e7-141">Determines whether the driver validates the certificate that is sent by the database server when SSL encryption is enabled (Encryption Method=1).</span><span class="sxs-lookup"><span data-stu-id="715e7-141">Determines whether the driver validates the certificate that is sent by the database server when SSL encryption is enabled (Encryption Method=1).</span></span> <span data-ttu-id="715e7-142">E.g.</span><span class="sxs-lookup"><span data-stu-id="715e7-142">E.g.</span></span> `ValidateServerCertificate=<0/1>;`| <span data-ttu-id="715e7-143">0 (Disabled) **(Default)** / 1 (Enabled)</span><span class="sxs-lookup"><span data-stu-id="715e7-143">0 (Disabled) **(Default)** / 1 (Enabled)</span></span> | <span data-ttu-id="715e7-144">No</span><span class="sxs-lookup"><span data-stu-id="715e7-144">No</span></span> |

<span data-ttu-id="715e7-145">**Example:**</span><span class="sxs-lookup"><span data-stu-id="715e7-145">**Example:**</span></span>

```json
{
    "name": "AzurePostgreSqlLinkedService",
    "properties": {
        "type": "AzurePostgreSql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>;Password=<Password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="715e7-146">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="715e7-146">Dataset properties</span></span>

<span data-ttu-id="715e7-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="715e7-147">For a full list of sections and properties available for defining datasets, see the [datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="715e7-148">This section provides a list of properties supported by Azure Database for PostgreSQL dataset.</span><span class="sxs-lookup"><span data-stu-id="715e7-148">This section provides a list of properties supported by Azure Database for PostgreSQL dataset.</span></span>

<span data-ttu-id="715e7-149">To copy data from Azure Database for PostgreSQL, set the type property of the dataset to **AzurePostgreSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="715e7-149">To copy data from Azure Database for PostgreSQL, set the type property of the dataset to **AzurePostgreSqlTable**.</span></span> <span data-ttu-id="715e7-150">There is no additional type-specific property in this type of dataset.</span><span class="sxs-lookup"><span data-stu-id="715e7-150">There is no additional type-specific property in this type of dataset.</span></span>

<span data-ttu-id="715e7-151">**Example**</span><span class="sxs-lookup"><span data-stu-id="715e7-151">**Example**</span></span>

```json
{
    "name": "AzurePostgreSqlDataset",
    "properties": {
        "type": "AzurePostgreSqlTable",
        "linkedServiceName": {
            "referenceName": "<AzurePostgreSql linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="715e7-152">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="715e7-152">Copy activity properties</span></span>

<span data-ttu-id="715e7-153">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="715e7-153">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="715e7-154">This section provides a list of properties supported by Azure Database for PostgreSQL source.</span><span class="sxs-lookup"><span data-stu-id="715e7-154">This section provides a list of properties supported by Azure Database for PostgreSQL source.</span></span>

### <a name="azurepostgresqlsource-as-source"></a><span data-ttu-id="715e7-155">AzurePostgreSqlSource as source</span><span class="sxs-lookup"><span data-stu-id="715e7-155">AzurePostgreSqlSource as source</span></span>

<span data-ttu-id="715e7-156">To copy data from Azure Database for PostgreSQL, set the source type in the copy activity to **AzurePostgreSqlSource**.</span><span class="sxs-lookup"><span data-stu-id="715e7-156">To copy data from Azure Database for PostgreSQL, set the source type in the copy activity to **AzurePostgreSqlSource**.</span></span> <span data-ttu-id="715e7-157">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="715e7-157">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="715e7-158">Property</span><span class="sxs-lookup"><span data-stu-id="715e7-158">Property</span></span> | <span data-ttu-id="715e7-159">Description</span><span class="sxs-lookup"><span data-stu-id="715e7-159">Description</span></span> | <span data-ttu-id="715e7-160">Required</span><span class="sxs-lookup"><span data-stu-id="715e7-160">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="715e7-161">type</span><span class="sxs-lookup"><span data-stu-id="715e7-161">type</span></span> | <span data-ttu-id="715e7-162">The type property of the copy activity source must be set to: **AzurePostgreSqlSource**</span><span class="sxs-lookup"><span data-stu-id="715e7-162">The type property of the copy activity source must be set to: **AzurePostgreSqlSource**</span></span> | <span data-ttu-id="715e7-163">Yes</span><span class="sxs-lookup"><span data-stu-id="715e7-163">Yes</span></span> |
| <span data-ttu-id="715e7-164">query</span><span class="sxs-lookup"><span data-stu-id="715e7-164">query</span></span> | <span data-ttu-id="715e7-165">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="715e7-165">Use the custom SQL query to read data.</span></span> <span data-ttu-id="715e7-166">For example: `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="715e7-166">For example: `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="715e7-167">Yes</span><span class="sxs-lookup"><span data-stu-id="715e7-167">Yes</span></span> |

<span data-ttu-id="715e7-168">**Example:**</span><span class="sxs-lookup"><span data-stu-id="715e7-168">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromAzurePostgreSql",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<AzurePostgreSql input dataset name>",
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
                "type": "AzurePostgreSqlSource",
                "query": "<custom query e.g. SELECT * FROM MyTable>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-azure-database-for-postgresql"></a><span data-ttu-id="715e7-169">Data type mapping for Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="715e7-169">Data type mapping for Azure Database for PostgreSQL</span></span>

<span data-ttu-id="715e7-170">When copying data from Azure Database for PostgreSQL, the following mappings are used from PostgreSQL data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="715e7-170">When copying data from Azure Database for PostgreSQL, the following mappings are used from PostgreSQL data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="715e7-171">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="715e7-171">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="715e7-172">PostgreSQL data type</span><span class="sxs-lookup"><span data-stu-id="715e7-172">PostgreSQL data type</span></span> | <span data-ttu-id="715e7-173">PostgresSQL aliases</span><span class="sxs-lookup"><span data-stu-id="715e7-173">PostgresSQL aliases</span></span> | <span data-ttu-id="715e7-174">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="715e7-174">Data factory interim data type</span></span> |
|:--- |:--- |:--- |
| `abstime` |&nbsp; |`String` |
| `bigint` | `int8` | `Int64` |
| `bigserial` | `serial8` | `Int64` |
| `bit [1]` |&nbsp; | `Boolean` |
| `bit [(n)], n>1` |&nbsp; | `Byte[]` |
| `bit varying [(n)]` | `varbit` |`Byte[]` |
| `boolean` | `bool` | `Boolean` |
| `box` |&nbsp; | `String` |
| `bytea` |&nbsp; | `Byte[], String` |
| `character [(n)]` | `char [(n)]` | `String` |
| `character varying [(n)]` | `varchar [(n)]` | `String` |
| `cid` |&nbsp; | `Int32` |
| `cidr` |&nbsp; | `String` |
| `circle` |&nbsp; |` String` |
| `date` |&nbsp; |`Datetime` |
| `daterange` |&nbsp; |`String` |
| `double precision` |`float8` |`Double` |
| `inet` |&nbsp; |`String` |
| `intarray` |&nbsp; |`String` |
| `int4range` |&nbsp; |`String` |
| `int8range` |&nbsp; |`String` |
| `integer` | `int, int4` |`Int32` |
| `interval [fields] [(p)]` | | `String` |
| `json` |&nbsp; | `String` |
| `jsonb` |&nbsp; | `Byte[]` |
| `line` |&nbsp; | `Byte[], String` |
| `lseg` |&nbsp; | `String` |
| `macaddr` |&nbsp; | `String` |
| `money` |&nbsp; | `String` |
| `numeric [(p, s)]`|`decimal [(p, s)]` |`String` |
| `numrange` |&nbsp; |`String` |
| `oid` |&nbsp; |`Int32` |
| `path` |&nbsp; |`String` |
| `pg_lsn` |&nbsp; |`Int64` |
| `point` |&nbsp; |`String` |
| `polygon` |&nbsp; |`String` |
| `real` |`float4` |`Single` |
| `smallint` |`int2` |`Int16` |
| `smallserial` |`serial2` |`Int16` |
| `serial` |`serial4` |`Int32` |
| `text` |&nbsp; |`String` |
| `timewithtimezone` |&nbsp; |`String` |
| `timewithouttimezone` |&nbsp; |`String` |
| `timestampwithtimezone` |&nbsp; |`String` |
| `xid` |&nbsp; |`Int32` |

## <a name="next-steps"></a><span data-ttu-id="715e7-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="715e7-175">Next steps</span></span>
<span data-ttu-id="715e7-176">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="715e7-176">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
