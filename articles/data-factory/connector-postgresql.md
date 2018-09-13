---
title: Copy data From PostgreSQL using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from PostgreSQL to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.openlocfilehash: 6279e088b8abd574bbd8ef6488d986d42c91123c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868870"
---
# <a name="copy-data-from-postgresql-by-using-azure-data-factory"></a><span data-ttu-id="1e3ac-103">Copy data from PostgreSQL by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1e3ac-103">Copy data from PostgreSQL by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-postgresql-connector.md)
> * [Current version](connector-postgresql.md)

<span data-ttu-id="1e3ac-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a PostgreSQL database.</span></span> <span data-ttu-id="1e3ac-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="1e3ac-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="1e3ac-108">Supported capabilities</span></span>

<span data-ttu-id="1e3ac-109">You can copy data from PostgreSQL database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-109">You can copy data from PostgreSQL database to any supported sink data store.</span></span> <span data-ttu-id="1e3ac-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="1e3ac-111">Specifically, this PostgreSQL connector supports PostgreSQL **version 7.4 and above**.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-111">Specifically, this PostgreSQL connector supports PostgreSQL **version 7.4 and above**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e3ac-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1e3ac-112">Prerequisites</span></span>

<span data-ttu-id="1e3ac-113">If your PostgreSQL database is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-113">If your PostgreSQL database is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="1e3ac-114">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-114">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span></span> <span data-ttu-id="1e3ac-115">The Integration Runtime provides a built-in PostgreSQL driver starting from version 3.7, therefore you don't need to manually install any driver.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-115">The Integration Runtime provides a built-in PostgreSQL driver starting from version 3.7, therefore you don't need to manually install any driver.</span></span>

<span data-ttu-id="1e3ac-116">For Self-hosted IR version lower than 3.7, you need to install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) with version between 2.0.12 and 3.1.9 on the Integration Runtime machine.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-116">For Self-hosted IR version lower than 3.7, you need to install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) with version between 2.0.12 and 3.1.9 on the Integration Runtime machine.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1e3ac-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="1e3ac-117">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="1e3ac-118">The following sections provide details about properties that are used to define Data Factory entities specific to PostgreSQL connector.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-118">The following sections provide details about properties that are used to define Data Factory entities specific to PostgreSQL connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1e3ac-119">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="1e3ac-119">Linked service properties</span></span>

<span data-ttu-id="1e3ac-120">The following properties are supported for PostgreSQL linked service:</span><span class="sxs-lookup"><span data-stu-id="1e3ac-120">The following properties are supported for PostgreSQL linked service:</span></span>

| <span data-ttu-id="1e3ac-121">Property</span><span class="sxs-lookup"><span data-stu-id="1e3ac-121">Property</span></span> | <span data-ttu-id="1e3ac-122">Description</span><span class="sxs-lookup"><span data-stu-id="1e3ac-122">Description</span></span> | <span data-ttu-id="1e3ac-123">Required</span><span class="sxs-lookup"><span data-stu-id="1e3ac-123">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1e3ac-124">type</span><span class="sxs-lookup"><span data-stu-id="1e3ac-124">type</span></span> | <span data-ttu-id="1e3ac-125">The type property must be set to: **PostgreSql**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-125">The type property must be set to: **PostgreSql**</span></span> | <span data-ttu-id="1e3ac-126">Yes</span><span class="sxs-lookup"><span data-stu-id="1e3ac-126">Yes</span></span> |
| <span data-ttu-id="1e3ac-127">connectionString</span><span class="sxs-lookup"><span data-stu-id="1e3ac-127">connectionString</span></span> | <span data-ttu-id="1e3ac-128">An ODBC connection string to connect to Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-128">An ODBC connection string to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="1e3ac-129">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1e3ac-129">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> | <span data-ttu-id="1e3ac-130">Yes</span><span class="sxs-lookup"><span data-stu-id="1e3ac-130">Yes</span></span> |
| <span data-ttu-id="1e3ac-131">connectVia</span><span class="sxs-lookup"><span data-stu-id="1e3ac-131">connectVia</span></span> | <span data-ttu-id="1e3ac-132">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-132">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="1e3ac-133">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="1e3ac-133">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="1e3ac-134">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-134">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="1e3ac-135">No</span><span class="sxs-lookup"><span data-stu-id="1e3ac-135">No</span></span> |

<span data-ttu-id="1e3ac-136">A typical connection string is `Server=<server>;Database=<database>;Port=<port>;UID=<username>;Password=<Password>`.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-136">A typical connection string is `Server=<server>;Database=<database>;Port=<port>;UID=<username>;Password=<Password>`.</span></span> <span data-ttu-id="1e3ac-137">More properties you can set per your case:</span><span class="sxs-lookup"><span data-stu-id="1e3ac-137">More properties you can set per your case:</span></span>

| <span data-ttu-id="1e3ac-138">Property</span><span class="sxs-lookup"><span data-stu-id="1e3ac-138">Property</span></span> | <span data-ttu-id="1e3ac-139">Description</span><span class="sxs-lookup"><span data-stu-id="1e3ac-139">Description</span></span> | <span data-ttu-id="1e3ac-140">Options</span><span class="sxs-lookup"><span data-stu-id="1e3ac-140">Options</span></span> | <span data-ttu-id="1e3ac-141">Required</span><span class="sxs-lookup"><span data-stu-id="1e3ac-141">Required</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="1e3ac-142">EncryptionMethod (EM)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-142">EncryptionMethod (EM)</span></span>| <span data-ttu-id="1e3ac-143">The method the driver uses to encrypt data sent between the driver and the database server.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-143">The method the driver uses to encrypt data sent between the driver and the database server.</span></span> <span data-ttu-id="1e3ac-144">E.g.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-144">E.g.</span></span> `ValidateServerCertificate=<0/1/6>;`| <span data-ttu-id="1e3ac-145">0 (No Encryption) **(Default)** / 1 (SSL) / 6 (RequestSSL)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-145">0 (No Encryption) **(Default)** / 1 (SSL) / 6 (RequestSSL)</span></span> | <span data-ttu-id="1e3ac-146">No</span><span class="sxs-lookup"><span data-stu-id="1e3ac-146">No</span></span> |
| <span data-ttu-id="1e3ac-147">ValidateServerCertificate (VSC)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-147">ValidateServerCertificate (VSC)</span></span> | <span data-ttu-id="1e3ac-148">Determines whether the driver validates the certificate that is sent by the database server when SSL encryption is enabled (Encryption Method=1).</span><span class="sxs-lookup"><span data-stu-id="1e3ac-148">Determines whether the driver validates the certificate that is sent by the database server when SSL encryption is enabled (Encryption Method=1).</span></span> <span data-ttu-id="1e3ac-149">E.g.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-149">E.g.</span></span> `ValidateServerCertificate=<0/1>;`| <span data-ttu-id="1e3ac-150">0 (Disabled) **(Default)** / 1 (Enabled)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-150">0 (Disabled) **(Default)** / 1 (Enabled)</span></span> | <span data-ttu-id="1e3ac-151">No</span><span class="sxs-lookup"><span data-stu-id="1e3ac-151">No</span></span> |

<span data-ttu-id="1e3ac-152">**Example:**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-152">**Example:**</span></span>

```json
{
    "name": "PostgreSqlLinkedService",
    "properties": {
        "type": "PostgreSql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>;Database=<database>;Port=<port>;UID=<username>;Password=<Password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="1e3ac-153">If you were using PostgreSQL linked service with the following payload, it is still supported as-is, while you are suggested to use the new one going forward.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-153">If you were using PostgreSQL linked service with the following payload, it is still supported as-is, while you are suggested to use the new one going forward.</span></span>

<span data-ttu-id="1e3ac-154">**Previous payload:**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-154">**Previous payload:**</span></span>

```json
{
    "name": "PostgreSqlLinkedService",
    "properties": {
        "type": "PostgreSql",
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

## <a name="dataset-properties"></a><span data-ttu-id="1e3ac-155">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="1e3ac-155">Dataset properties</span></span>

<span data-ttu-id="1e3ac-156">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-156">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="1e3ac-157">This section provides a list of properties supported by PostgreSQL dataset.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-157">This section provides a list of properties supported by PostgreSQL dataset.</span></span>

<span data-ttu-id="1e3ac-158">To copy data from PostgreSQL, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-158">To copy data from PostgreSQL, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="1e3ac-159">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="1e3ac-159">The following properties are supported:</span></span>

| <span data-ttu-id="1e3ac-160">Property</span><span class="sxs-lookup"><span data-stu-id="1e3ac-160">Property</span></span> | <span data-ttu-id="1e3ac-161">Description</span><span class="sxs-lookup"><span data-stu-id="1e3ac-161">Description</span></span> | <span data-ttu-id="1e3ac-162">Required</span><span class="sxs-lookup"><span data-stu-id="1e3ac-162">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1e3ac-163">type</span><span class="sxs-lookup"><span data-stu-id="1e3ac-163">type</span></span> | <span data-ttu-id="1e3ac-164">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-164">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="1e3ac-165">Yes</span><span class="sxs-lookup"><span data-stu-id="1e3ac-165">Yes</span></span> |
| <span data-ttu-id="1e3ac-166">tableName</span><span class="sxs-lookup"><span data-stu-id="1e3ac-166">tableName</span></span> | <span data-ttu-id="1e3ac-167">Name of the table in the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-167">Name of the table in the PostgreSQL database.</span></span> | <span data-ttu-id="1e3ac-168">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-168">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="1e3ac-169">**Example**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-169">**Example**</span></span>

```json
{
    "name": "PostgreSQLDataset",
    "properties":
    {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<PostgreSQL linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="1e3ac-170">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="1e3ac-170">Copy activity properties</span></span>

<span data-ttu-id="1e3ac-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="1e3ac-172">This section provides a list of properties supported by PostgreSQL source.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-172">This section provides a list of properties supported by PostgreSQL source.</span></span>

### <a name="postgresql-as-source"></a><span data-ttu-id="1e3ac-173">PostgreSQL as source</span><span class="sxs-lookup"><span data-stu-id="1e3ac-173">PostgreSQL as source</span></span>

<span data-ttu-id="1e3ac-174">To copy data from PostgreSQL, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-174">To copy data from PostgreSQL, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="1e3ac-175">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="1e3ac-175">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="1e3ac-176">Property</span><span class="sxs-lookup"><span data-stu-id="1e3ac-176">Property</span></span> | <span data-ttu-id="1e3ac-177">Description</span><span class="sxs-lookup"><span data-stu-id="1e3ac-177">Description</span></span> | <span data-ttu-id="1e3ac-178">Required</span><span class="sxs-lookup"><span data-stu-id="1e3ac-178">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1e3ac-179">type</span><span class="sxs-lookup"><span data-stu-id="1e3ac-179">type</span></span> | <span data-ttu-id="1e3ac-180">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-180">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="1e3ac-181">Yes</span><span class="sxs-lookup"><span data-stu-id="1e3ac-181">Yes</span></span> |
| <span data-ttu-id="1e3ac-182">query</span><span class="sxs-lookup"><span data-stu-id="1e3ac-182">query</span></span> | <span data-ttu-id="1e3ac-183">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-183">Use the custom SQL query to read data.</span></span> <span data-ttu-id="1e3ac-184">For example: `"query": "SELECT * FROM \"MySchema\".\"MyTable\""`.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-184">For example: `"query": "SELECT * FROM \"MySchema\".\"MyTable\""`.</span></span> | <span data-ttu-id="1e3ac-185">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="1e3ac-185">No (if "tableName" in dataset is specified)</span></span> |

> [!NOTE]
> Schema and table names are case-sensitive. Enclose them in `""` (double quotes) in the query.

<span data-ttu-id="1e3ac-188">**Example:**</span><span class="sxs-lookup"><span data-stu-id="1e3ac-188">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromPostgreSQL",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<PostgreSQL input dataset name>",
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
                "query": "SELECT * FROM \"MySchema\".\"MyTable\""
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-postgresql"></a><span data-ttu-id="1e3ac-189">Data type mapping for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1e3ac-189">Data type mapping for PostgreSQL</span></span>

<span data-ttu-id="1e3ac-190">When copying data from PostgreSQL, the following mappings are used from PostgreSQL data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-190">When copying data from PostgreSQL, the following mappings are used from PostgreSQL data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="1e3ac-191">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="1e3ac-191">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="1e3ac-192">PostgreSQL data type</span><span class="sxs-lookup"><span data-stu-id="1e3ac-192">PostgreSQL data type</span></span> | <span data-ttu-id="1e3ac-193">PostgresSQL aliases</span><span class="sxs-lookup"><span data-stu-id="1e3ac-193">PostgresSQL aliases</span></span> | <span data-ttu-id="1e3ac-194">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="1e3ac-194">Data factory interim data type</span></span> |
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

## <a name="next-steps"></a><span data-ttu-id="1e3ac-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e3ac-195">Next steps</span></span>
<span data-ttu-id="1e3ac-196">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1e3ac-196">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
