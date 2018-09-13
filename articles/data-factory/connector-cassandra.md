---
title: Copy data from Cassandra using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Cassandra to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/07/2018
ms.author: jingwang
ms.openlocfilehash: a0095ae4aa50845a24cabb981399ac4035afdebe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871537"
---
# <a name="copy-data-from-cassandra-using-azure-data-factory"></a><span data-ttu-id="8bc61-103">Copy data from Cassandra using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8bc61-103">Copy data from Cassandra using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-cassandra-connector.md)
> * [Current version](connector-cassandra.md)

<span data-ttu-id="8bc61-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="8bc61-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a Cassandra database.</span></span> <span data-ttu-id="8bc61-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="8bc61-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="8bc61-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="8bc61-108">Supported capabilities</span></span>

<span data-ttu-id="8bc61-109">You can copy data from Cassandra database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="8bc61-109">You can copy data from Cassandra database to any supported sink data store.</span></span> <span data-ttu-id="8bc61-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="8bc61-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="8bc61-111">Specifically, this Cassandra connector supports:</span><span class="sxs-lookup"><span data-stu-id="8bc61-111">Specifically, this Cassandra connector supports:</span></span>

- <span data-ttu-id="8bc61-112">Cassandra **versions 2.x and 3.x**.</span><span class="sxs-lookup"><span data-stu-id="8bc61-112">Cassandra **versions 2.x and 3.x**.</span></span>
- <span data-ttu-id="8bc61-113">Copying data using **Basic** or **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="8bc61-113">Copying data using **Basic** or **Anonymous** authentication.</span></span>

>[!NOTE]
>For activity running on Self-hosted Integration Runtime, Cassandra 3.x is supported since IR version 3.7 and above.

## <a name="prerequisites"></a><span data-ttu-id="8bc61-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8bc61-115">Prerequisites</span></span>

<span data-ttu-id="8bc61-116">To copy data from a Cassandra database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="8bc61-116">To copy data from a Cassandra database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="8bc61-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article to learn details.</span><span class="sxs-lookup"><span data-stu-id="8bc61-117">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article to learn details.</span></span> <span data-ttu-id="8bc61-118">The Integration Runtime provides a built-in Cassandra driver, therefore you don't need to manually install any driver when copying data from/to Cassandra.</span><span class="sxs-lookup"><span data-stu-id="8bc61-118">The Integration Runtime provides a built-in Cassandra driver, therefore you don't need to manually install any driver when copying data from/to Cassandra.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8bc61-119">Getting started</span><span class="sxs-lookup"><span data-stu-id="8bc61-119">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="8bc61-120">The following sections provide details about properties that are used to define Data Factory entities specific to Cassandra connector.</span><span class="sxs-lookup"><span data-stu-id="8bc61-120">The following sections provide details about properties that are used to define Data Factory entities specific to Cassandra connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8bc61-121">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="8bc61-121">Linked service properties</span></span>

<span data-ttu-id="8bc61-122">The following properties are supported for Cassandra linked service:</span><span class="sxs-lookup"><span data-stu-id="8bc61-122">The following properties are supported for Cassandra linked service:</span></span>

| <span data-ttu-id="8bc61-123">Property</span><span class="sxs-lookup"><span data-stu-id="8bc61-123">Property</span></span> | <span data-ttu-id="8bc61-124">Description</span><span class="sxs-lookup"><span data-stu-id="8bc61-124">Description</span></span> | <span data-ttu-id="8bc61-125">Required</span><span class="sxs-lookup"><span data-stu-id="8bc61-125">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8bc61-126">type</span><span class="sxs-lookup"><span data-stu-id="8bc61-126">type</span></span> |<span data-ttu-id="8bc61-127">The type property must be set to: **Cassandra**</span><span class="sxs-lookup"><span data-stu-id="8bc61-127">The type property must be set to: **Cassandra**</span></span> |<span data-ttu-id="8bc61-128">Yes</span><span class="sxs-lookup"><span data-stu-id="8bc61-128">Yes</span></span> |
| <span data-ttu-id="8bc61-129">host</span><span class="sxs-lookup"><span data-stu-id="8bc61-129">host</span></span> |<span data-ttu-id="8bc61-130">One or more IP addresses or host names of Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="8bc61-130">One or more IP addresses or host names of Cassandra servers.</span></span><br/><span data-ttu-id="8bc61-131">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span><span class="sxs-lookup"><span data-stu-id="8bc61-131">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="8bc61-132">Yes</span><span class="sxs-lookup"><span data-stu-id="8bc61-132">Yes</span></span> |
| <span data-ttu-id="8bc61-133">port</span><span class="sxs-lookup"><span data-stu-id="8bc61-133">port</span></span> |<span data-ttu-id="8bc61-134">The TCP port that the Cassandra server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="8bc61-134">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="8bc61-135">No (default is 9042)</span><span class="sxs-lookup"><span data-stu-id="8bc61-135">No (default is 9042)</span></span> |
| <span data-ttu-id="8bc61-136">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8bc61-136">authenticationType</span></span> | <span data-ttu-id="8bc61-137">Type of authentication used to connect to the Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="8bc61-137">Type of authentication used to connect to the Cassandra database.</span></span><br/><span data-ttu-id="8bc61-138">Allowed values are: **Basic**, and **Anonymous**.</span><span class="sxs-lookup"><span data-stu-id="8bc61-138">Allowed values are: **Basic**, and **Anonymous**.</span></span> |<span data-ttu-id="8bc61-139">Yes</span><span class="sxs-lookup"><span data-stu-id="8bc61-139">Yes</span></span> |
| <span data-ttu-id="8bc61-140">username</span><span class="sxs-lookup"><span data-stu-id="8bc61-140">username</span></span> |<span data-ttu-id="8bc61-141">Specify user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="8bc61-141">Specify user name for the user account.</span></span> |<span data-ttu-id="8bc61-142">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="8bc61-142">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="8bc61-143">password</span><span class="sxs-lookup"><span data-stu-id="8bc61-143">password</span></span> |<span data-ttu-id="8bc61-144">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="8bc61-144">Specify password for the user account.</span></span> <span data-ttu-id="8bc61-145">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8bc61-145">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="8bc61-146">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="8bc61-146">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="8bc61-147">connectVia</span><span class="sxs-lookup"><span data-stu-id="8bc61-147">connectVia</span></span> | <span data-ttu-id="8bc61-148">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="8bc61-148">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="8bc61-149">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="8bc61-149">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="8bc61-150">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="8bc61-150">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="8bc61-151">No</span><span class="sxs-lookup"><span data-stu-id="8bc61-151">No</span></span> |

>[!NOTE]
>Currently connection to Cassandra using SSL is not supported.

<span data-ttu-id="8bc61-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="8bc61-153">**Example:**</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "Cassandra",
        "typeProperties": {
            "host": "<host>",
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

## <a name="dataset-properties"></a><span data-ttu-id="8bc61-154">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="8bc61-154">Dataset properties</span></span>

<span data-ttu-id="8bc61-155">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="8bc61-155">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="8bc61-156">This section provides a list of properties supported by Cassandra dataset.</span><span class="sxs-lookup"><span data-stu-id="8bc61-156">This section provides a list of properties supported by Cassandra dataset.</span></span>

<span data-ttu-id="8bc61-157">To copy data from Cassandra, set the type property of the dataset to **CassandraTable**.</span><span class="sxs-lookup"><span data-stu-id="8bc61-157">To copy data from Cassandra, set the type property of the dataset to **CassandraTable**.</span></span> <span data-ttu-id="8bc61-158">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="8bc61-158">The following properties are supported:</span></span>

| <span data-ttu-id="8bc61-159">Property</span><span class="sxs-lookup"><span data-stu-id="8bc61-159">Property</span></span> | <span data-ttu-id="8bc61-160">Description</span><span class="sxs-lookup"><span data-stu-id="8bc61-160">Description</span></span> | <span data-ttu-id="8bc61-161">Required</span><span class="sxs-lookup"><span data-stu-id="8bc61-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8bc61-162">type</span><span class="sxs-lookup"><span data-stu-id="8bc61-162">type</span></span> | <span data-ttu-id="8bc61-163">The type property of the dataset must be set to: **CassandraTable**</span><span class="sxs-lookup"><span data-stu-id="8bc61-163">The type property of the dataset must be set to: **CassandraTable**</span></span> | <span data-ttu-id="8bc61-164">Yes</span><span class="sxs-lookup"><span data-stu-id="8bc61-164">Yes</span></span> |
| <span data-ttu-id="8bc61-165">keyspace</span><span class="sxs-lookup"><span data-stu-id="8bc61-165">keyspace</span></span> |<span data-ttu-id="8bc61-166">Name of the keyspace or schema in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="8bc61-166">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="8bc61-167">No (if "query" for "CassandraSource" is specified)</span><span class="sxs-lookup"><span data-stu-id="8bc61-167">No (if "query" for "CassandraSource" is specified)</span></span> |
| <span data-ttu-id="8bc61-168">tableName</span><span class="sxs-lookup"><span data-stu-id="8bc61-168">tableName</span></span> |<span data-ttu-id="8bc61-169">Name of the table in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="8bc61-169">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="8bc61-170">No (if "query" for "CassandraSource" is specified)</span><span class="sxs-lookup"><span data-stu-id="8bc61-170">No (if "query" for "CassandraSource" is specified)</span></span> |

<span data-ttu-id="8bc61-171">**Example:**</span><span class="sxs-lookup"><span data-stu-id="8bc61-171">**Example:**</span></span>

```json
{
    "name": "CassandraDataset",
    "properties": {
        "type": "CassandraTable",
        "linkedServiceName": {
            "referenceName": "<Cassandra linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "keySpace": "<keyspace name>",
            "tableName": "<table name>"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="8bc61-172">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="8bc61-172">Copy activity properties</span></span>


<span data-ttu-id="8bc61-173">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="8bc61-173">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="8bc61-174">This section provides a list of properties supported by Cassandra source.</span><span class="sxs-lookup"><span data-stu-id="8bc61-174">This section provides a list of properties supported by Cassandra source.</span></span>

### <a name="cassandra-as-source"></a><span data-ttu-id="8bc61-175">Cassandra as source</span><span class="sxs-lookup"><span data-stu-id="8bc61-175">Cassandra as source</span></span>

<span data-ttu-id="8bc61-176">To copy data from Cassandra, set the source type in the copy activity to **CassandraSource**.</span><span class="sxs-lookup"><span data-stu-id="8bc61-176">To copy data from Cassandra, set the source type in the copy activity to **CassandraSource**.</span></span> <span data-ttu-id="8bc61-177">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="8bc61-177">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="8bc61-178">Property</span><span class="sxs-lookup"><span data-stu-id="8bc61-178">Property</span></span> | <span data-ttu-id="8bc61-179">Description</span><span class="sxs-lookup"><span data-stu-id="8bc61-179">Description</span></span> | <span data-ttu-id="8bc61-180">Required</span><span class="sxs-lookup"><span data-stu-id="8bc61-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8bc61-181">type</span><span class="sxs-lookup"><span data-stu-id="8bc61-181">type</span></span> | <span data-ttu-id="8bc61-182">The type property of the copy activity source must be set to: **CassandraSource**</span><span class="sxs-lookup"><span data-stu-id="8bc61-182">The type property of the copy activity source must be set to: **CassandraSource**</span></span> | <span data-ttu-id="8bc61-183">Yes</span><span class="sxs-lookup"><span data-stu-id="8bc61-183">Yes</span></span> |
| <span data-ttu-id="8bc61-184">query</span><span class="sxs-lookup"><span data-stu-id="8bc61-184">query</span></span> |<span data-ttu-id="8bc61-185">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="8bc61-185">Use the custom query to read data.</span></span> |<span data-ttu-id="8bc61-186">SQL-92 query or CQL query.</span><span class="sxs-lookup"><span data-stu-id="8bc61-186">SQL-92 query or CQL query.</span></span> <span data-ttu-id="8bc61-187">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="8bc61-187">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="8bc61-188">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span><span class="sxs-lookup"><span data-stu-id="8bc61-188">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="8bc61-189">No (if "tableName" and "keyspace" in dataset are specified).</span><span class="sxs-lookup"><span data-stu-id="8bc61-189">No (if "tableName" and "keyspace" in dataset are specified).</span></span> |
| <span data-ttu-id="8bc61-190">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="8bc61-190">consistencyLevel</span></span> |<span data-ttu-id="8bc61-191">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span><span class="sxs-lookup"><span data-stu-id="8bc61-191">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="8bc61-192">Cassandra checks the specified number of replicas for data to satisfy the read request.</span><span class="sxs-lookup"><span data-stu-id="8bc61-192">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> <span data-ttu-id="8bc61-193">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span><span class="sxs-lookup"><span data-stu-id="8bc61-193">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span></span><br/><br/><span data-ttu-id="8bc61-194">Allowed values are: **ONE**, **TWO**, **THREE**, **QUORUM**, **ALL**, **LOCAL_QUORUM**, **EACH_QUORUM**, and **LOCAL_ONE**.</span><span class="sxs-lookup"><span data-stu-id="8bc61-194">Allowed values are: **ONE**, **TWO**, **THREE**, **QUORUM**, **ALL**, **LOCAL_QUORUM**, **EACH_QUORUM**, and **LOCAL_ONE**.</span></span> |<span data-ttu-id="8bc61-195">No (default is `ONE`)</span><span class="sxs-lookup"><span data-stu-id="8bc61-195">No (default is `ONE`)</span></span> |

<span data-ttu-id="8bc61-196">**Example:**</span><span class="sxs-lookup"><span data-stu-id="8bc61-196">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromCassandra",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Cassandra input dataset name>",
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
                "type": "CassandraSource",
                "query": "select id, firstname, lastname from mykeyspace.mytable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-cassandra"></a><span data-ttu-id="8bc61-197">Data type mapping for Cassandra</span><span class="sxs-lookup"><span data-stu-id="8bc61-197">Data type mapping for Cassandra</span></span>

<span data-ttu-id="8bc61-198">When copying data from Cassandra, the following mappings are used from Cassandra data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="8bc61-198">When copying data from Cassandra, the following mappings are used from Cassandra data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="8bc61-199">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="8bc61-199">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="8bc61-200">Cassandra data type</span><span class="sxs-lookup"><span data-stu-id="8bc61-200">Cassandra data type</span></span> | <span data-ttu-id="8bc61-201">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="8bc61-201">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="8bc61-202">ASCII</span><span class="sxs-lookup"><span data-stu-id="8bc61-202">ASCII</span></span> |<span data-ttu-id="8bc61-203">String</span><span class="sxs-lookup"><span data-stu-id="8bc61-203">String</span></span> |
| <span data-ttu-id="8bc61-204">BIGINT</span><span class="sxs-lookup"><span data-stu-id="8bc61-204">BIGINT</span></span> |<span data-ttu-id="8bc61-205">Int64</span><span class="sxs-lookup"><span data-stu-id="8bc61-205">Int64</span></span> |
| <span data-ttu-id="8bc61-206">BLOB</span><span class="sxs-lookup"><span data-stu-id="8bc61-206">BLOB</span></span> |<span data-ttu-id="8bc61-207">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8bc61-207">Byte[]</span></span> |
| <span data-ttu-id="8bc61-208">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="8bc61-208">BOOLEAN</span></span> |<span data-ttu-id="8bc61-209">Boolean</span><span class="sxs-lookup"><span data-stu-id="8bc61-209">Boolean</span></span> |
| <span data-ttu-id="8bc61-210">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="8bc61-210">DECIMAL</span></span> |<span data-ttu-id="8bc61-211">Decimal</span><span class="sxs-lookup"><span data-stu-id="8bc61-211">Decimal</span></span> |
| <span data-ttu-id="8bc61-212">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="8bc61-212">DOUBLE</span></span> |<span data-ttu-id="8bc61-213">Double</span><span class="sxs-lookup"><span data-stu-id="8bc61-213">Double</span></span> |
| <span data-ttu-id="8bc61-214">FLOAT</span><span class="sxs-lookup"><span data-stu-id="8bc61-214">FLOAT</span></span> |<span data-ttu-id="8bc61-215">Single</span><span class="sxs-lookup"><span data-stu-id="8bc61-215">Single</span></span> |
| <span data-ttu-id="8bc61-216">INET</span><span class="sxs-lookup"><span data-stu-id="8bc61-216">INET</span></span> |<span data-ttu-id="8bc61-217">String</span><span class="sxs-lookup"><span data-stu-id="8bc61-217">String</span></span> |
| <span data-ttu-id="8bc61-218">INT</span><span class="sxs-lookup"><span data-stu-id="8bc61-218">INT</span></span> |<span data-ttu-id="8bc61-219">Int32</span><span class="sxs-lookup"><span data-stu-id="8bc61-219">Int32</span></span> |
| <span data-ttu-id="8bc61-220">TEXT</span><span class="sxs-lookup"><span data-stu-id="8bc61-220">TEXT</span></span> |<span data-ttu-id="8bc61-221">String</span><span class="sxs-lookup"><span data-stu-id="8bc61-221">String</span></span> |
| <span data-ttu-id="8bc61-222">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="8bc61-222">TIMESTAMP</span></span> |<span data-ttu-id="8bc61-223">DateTime</span><span class="sxs-lookup"><span data-stu-id="8bc61-223">DateTime</span></span> |
| <span data-ttu-id="8bc61-224">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="8bc61-224">TIMEUUID</span></span> |<span data-ttu-id="8bc61-225">Guid</span><span class="sxs-lookup"><span data-stu-id="8bc61-225">Guid</span></span> |
| <span data-ttu-id="8bc61-226">UUID</span><span class="sxs-lookup"><span data-stu-id="8bc61-226">UUID</span></span> |<span data-ttu-id="8bc61-227">Guid</span><span class="sxs-lookup"><span data-stu-id="8bc61-227">Guid</span></span> |
| <span data-ttu-id="8bc61-228">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="8bc61-228">VARCHAR</span></span> |<span data-ttu-id="8bc61-229">String</span><span class="sxs-lookup"><span data-stu-id="8bc61-229">String</span></span> |
| <span data-ttu-id="8bc61-230">VARINT</span><span class="sxs-lookup"><span data-stu-id="8bc61-230">VARINT</span></span> |<span data-ttu-id="8bc61-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="8bc61-231">Decimal</span></span> |

> [!NOTE]
> For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.
>
> User-defined types are not supported.
>
> The length of Binary Column and String Column lengths cannot be greater than 4000.
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="8bc61-235">Work with collections using virtual table</span><span class="sxs-lookup"><span data-stu-id="8bc61-235">Work with collections using virtual table</span></span>

<span data-ttu-id="8bc61-236">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="8bc61-236">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="8bc61-237">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span><span class="sxs-lookup"><span data-stu-id="8bc61-237">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="8bc61-238">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span><span class="sxs-lookup"><span data-stu-id="8bc61-238">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="8bc61-239">A **base table**, which contains the same data as the real table except for the collection columns.</span><span class="sxs-lookup"><span data-stu-id="8bc61-239">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="8bc61-240">The base table uses the same name as the real table that it represents.</span><span class="sxs-lookup"><span data-stu-id="8bc61-240">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="8bc61-241">A **virtual table** for each collection column, which expands the nested data.</span><span class="sxs-lookup"><span data-stu-id="8bc61-241">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="8bc61-242">The virtual tables that represent collections are named using the name of the real table, a separator "*vt*" and the name of the column.</span><span class="sxs-lookup"><span data-stu-id="8bc61-242">The virtual tables that represent collections are named using the name of the real table, a separator "*vt*" and the name of the column.</span></span>

<span data-ttu-id="8bc61-243">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span><span class="sxs-lookup"><span data-stu-id="8bc61-243">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="8bc61-244">See Example section for details.</span><span class="sxs-lookup"><span data-stu-id="8bc61-244">See Example section for details.</span></span> <span data-ttu-id="8bc61-245">You can access the content of Cassandra collections by querying and joining the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="8bc61-245">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

### <a name="example"></a><span data-ttu-id="8bc61-246">Example</span><span class="sxs-lookup"><span data-stu-id="8bc61-246">Example</span></span>

<span data-ttu-id="8bc61-247">For example, the following "ExampleTable" is a Cassandra database table that contains an integer primary key column named "pk_int", a text column named value, a list column, a map column, and a set column (named "StringSet").</span><span class="sxs-lookup"><span data-stu-id="8bc61-247">For example, the following "ExampleTable" is a Cassandra database table that contains an integer primary key column named "pk_int", a text column named value, a list column, a map column, and a set column (named "StringSet").</span></span>

| <span data-ttu-id="8bc61-248">pk_int</span><span class="sxs-lookup"><span data-stu-id="8bc61-248">pk_int</span></span> | <span data-ttu-id="8bc61-249">Value</span><span class="sxs-lookup"><span data-stu-id="8bc61-249">Value</span></span> | <span data-ttu-id="8bc61-250">List</span><span class="sxs-lookup"><span data-stu-id="8bc61-250">List</span></span> | <span data-ttu-id="8bc61-251">Map</span><span class="sxs-lookup"><span data-stu-id="8bc61-251">Map</span></span> | <span data-ttu-id="8bc61-252">StringSet</span><span class="sxs-lookup"><span data-stu-id="8bc61-252">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8bc61-253">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-253">1</span></span> |<span data-ttu-id="8bc61-254">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="8bc61-254">"sample value 1"</span></span> |<span data-ttu-id="8bc61-255">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="8bc61-255">["1", "2", "3"]</span></span> |<span data-ttu-id="8bc61-256">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="8bc61-256">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="8bc61-257">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="8bc61-257">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="8bc61-258">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-258">3</span></span> |<span data-ttu-id="8bc61-259">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="8bc61-259">"sample value 3"</span></span> |<span data-ttu-id="8bc61-260">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="8bc61-260">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="8bc61-261">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="8bc61-261">{"S1": "t"}</span></span> |<span data-ttu-id="8bc61-262">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="8bc61-262">{"A", "E"}</span></span> |

<span data-ttu-id="8bc61-263">The driver would generate multiple virtual tables to represent this single table.</span><span class="sxs-lookup"><span data-stu-id="8bc61-263">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="8bc61-264">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span><span class="sxs-lookup"><span data-stu-id="8bc61-264">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="8bc61-265">The first virtual table is the base table named "ExampleTable" is shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="8bc61-265">The first virtual table is the base table named "ExampleTable" is shown in the following table:</span></span> 

| <span data-ttu-id="8bc61-266">pk_int</span><span class="sxs-lookup"><span data-stu-id="8bc61-266">pk_int</span></span> | <span data-ttu-id="8bc61-267">Value</span><span class="sxs-lookup"><span data-stu-id="8bc61-267">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8bc61-268">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-268">1</span></span> |<span data-ttu-id="8bc61-269">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="8bc61-269">"sample value 1"</span></span> |
| <span data-ttu-id="8bc61-270">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-270">3</span></span> |<span data-ttu-id="8bc61-271">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="8bc61-271">"sample value 3"</span></span> |

<span data-ttu-id="8bc61-272">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span><span class="sxs-lookup"><span data-stu-id="8bc61-272">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

<span data-ttu-id="8bc61-273">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span><span class="sxs-lookup"><span data-stu-id="8bc61-273">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="8bc61-274">The columns with names that end with "_index" or "_key" indicate the position of the data within the original list or map.</span><span class="sxs-lookup"><span data-stu-id="8bc61-274">The columns with names that end with "_index" or "_key" indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="8bc61-275">The columns with names that end with "_value" contain the expanded data from the collection.</span><span class="sxs-lookup"><span data-stu-id="8bc61-275">The columns with names that end with "_value" contain the expanded data from the collection.</span></span>

<span data-ttu-id="8bc61-276">**Table "ExampleTable_vt_List":**</span><span class="sxs-lookup"><span data-stu-id="8bc61-276">**Table "ExampleTable_vt_List":**</span></span>

| <span data-ttu-id="8bc61-277">pk_int</span><span class="sxs-lookup"><span data-stu-id="8bc61-277">pk_int</span></span> | <span data-ttu-id="8bc61-278">List_index</span><span class="sxs-lookup"><span data-stu-id="8bc61-278">List_index</span></span> | <span data-ttu-id="8bc61-279">List_value</span><span class="sxs-lookup"><span data-stu-id="8bc61-279">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bc61-280">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-280">1</span></span> |<span data-ttu-id="8bc61-281">0</span><span class="sxs-lookup"><span data-stu-id="8bc61-281">0</span></span> |<span data-ttu-id="8bc61-282">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-282">1</span></span> |
| <span data-ttu-id="8bc61-283">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-283">1</span></span> |<span data-ttu-id="8bc61-284">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-284">1</span></span> |<span data-ttu-id="8bc61-285">2</span><span class="sxs-lookup"><span data-stu-id="8bc61-285">2</span></span> |
| <span data-ttu-id="8bc61-286">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-286">1</span></span> |<span data-ttu-id="8bc61-287">2</span><span class="sxs-lookup"><span data-stu-id="8bc61-287">2</span></span> |<span data-ttu-id="8bc61-288">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-288">3</span></span> |
| <span data-ttu-id="8bc61-289">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-289">3</span></span> |<span data-ttu-id="8bc61-290">0</span><span class="sxs-lookup"><span data-stu-id="8bc61-290">0</span></span> |<span data-ttu-id="8bc61-291">100</span><span class="sxs-lookup"><span data-stu-id="8bc61-291">100</span></span> |
| <span data-ttu-id="8bc61-292">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-292">3</span></span> |<span data-ttu-id="8bc61-293">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-293">1</span></span> |<span data-ttu-id="8bc61-294">101</span><span class="sxs-lookup"><span data-stu-id="8bc61-294">101</span></span> |
| <span data-ttu-id="8bc61-295">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-295">3</span></span> |<span data-ttu-id="8bc61-296">2</span><span class="sxs-lookup"><span data-stu-id="8bc61-296">2</span></span> |<span data-ttu-id="8bc61-297">102</span><span class="sxs-lookup"><span data-stu-id="8bc61-297">102</span></span> |
| <span data-ttu-id="8bc61-298">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-298">3</span></span> |<span data-ttu-id="8bc61-299">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-299">3</span></span> |<span data-ttu-id="8bc61-300">103</span><span class="sxs-lookup"><span data-stu-id="8bc61-300">103</span></span> |

<span data-ttu-id="8bc61-301">**Table "ExampleTable_vt_Map":**</span><span class="sxs-lookup"><span data-stu-id="8bc61-301">**Table "ExampleTable_vt_Map":**</span></span>

| <span data-ttu-id="8bc61-302">pk_int</span><span class="sxs-lookup"><span data-stu-id="8bc61-302">pk_int</span></span> | <span data-ttu-id="8bc61-303">Map_key</span><span class="sxs-lookup"><span data-stu-id="8bc61-303">Map_key</span></span> | <span data-ttu-id="8bc61-304">Map_value</span><span class="sxs-lookup"><span data-stu-id="8bc61-304">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bc61-305">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-305">1</span></span> |<span data-ttu-id="8bc61-306">S1</span><span class="sxs-lookup"><span data-stu-id="8bc61-306">S1</span></span> |<span data-ttu-id="8bc61-307">A</span><span class="sxs-lookup"><span data-stu-id="8bc61-307">A</span></span> |
| <span data-ttu-id="8bc61-308">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-308">1</span></span> |<span data-ttu-id="8bc61-309">S2</span><span class="sxs-lookup"><span data-stu-id="8bc61-309">S2</span></span> |<span data-ttu-id="8bc61-310">b</span><span class="sxs-lookup"><span data-stu-id="8bc61-310">b</span></span> |
| <span data-ttu-id="8bc61-311">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-311">3</span></span> |<span data-ttu-id="8bc61-312">S1</span><span class="sxs-lookup"><span data-stu-id="8bc61-312">S1</span></span> |<span data-ttu-id="8bc61-313">t</span><span class="sxs-lookup"><span data-stu-id="8bc61-313">t</span></span> |

<span data-ttu-id="8bc61-314">**Table "ExampleTable_vt_StringSet":**</span><span class="sxs-lookup"><span data-stu-id="8bc61-314">**Table "ExampleTable_vt_StringSet":**</span></span>

| <span data-ttu-id="8bc61-315">pk_int</span><span class="sxs-lookup"><span data-stu-id="8bc61-315">pk_int</span></span> | <span data-ttu-id="8bc61-316">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="8bc61-316">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="8bc61-317">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-317">1</span></span> |<span data-ttu-id="8bc61-318">A</span><span class="sxs-lookup"><span data-stu-id="8bc61-318">A</span></span> |
| <span data-ttu-id="8bc61-319">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-319">1</span></span> |<span data-ttu-id="8bc61-320">B</span><span class="sxs-lookup"><span data-stu-id="8bc61-320">B</span></span> |
| <span data-ttu-id="8bc61-321">1</span><span class="sxs-lookup"><span data-stu-id="8bc61-321">1</span></span> |<span data-ttu-id="8bc61-322">C</span><span class="sxs-lookup"><span data-stu-id="8bc61-322">C</span></span> |
| <span data-ttu-id="8bc61-323">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-323">3</span></span> |<span data-ttu-id="8bc61-324">A</span><span class="sxs-lookup"><span data-stu-id="8bc61-324">A</span></span> |
| <span data-ttu-id="8bc61-325">3</span><span class="sxs-lookup"><span data-stu-id="8bc61-325">3</span></span> |<span data-ttu-id="8bc61-326">E</span><span class="sxs-lookup"><span data-stu-id="8bc61-326">E</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8bc61-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bc61-327">Next steps</span></span>
<span data-ttu-id="8bc61-328">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8bc61-328">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
