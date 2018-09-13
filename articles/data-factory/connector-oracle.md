---
title: Copy data to and from Oracle by using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from supported source stores to an Oracle database or from Oracle to supported sink stores by using Data Factory.
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
ms.date: 06/14/2018
ms.author: jingwang
ms.openlocfilehash: ec0fc11ac2caf421f331a8fe72f1dacdf6b8a702
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856840"
---
# <a name="copy-data-from-and-to-oracle-by-using-azure-data-factory"></a><span data-ttu-id="aa5ed-103">Copy data from and to Oracle by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="aa5ed-103">Copy data from and to Oracle by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-oracle-connector.md)
> * [Current version](connector-oracle.md)

<span data-ttu-id="aa5ed-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to an Oracle database.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-106">This article outlines how to use Copy Activity in Azure Data Factory to copy data from and to an Oracle database.</span></span> <span data-ttu-id="aa5ed-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-107">It builds on the [Copy Activity overview](copy-activity-overview.md) article that presents a general overview of the copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="aa5ed-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="aa5ed-108">Supported capabilities</span></span>

<span data-ttu-id="aa5ed-109">You can copy data from an Oracle database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-109">You can copy data from an Oracle database to any supported sink data store.</span></span> <span data-ttu-id="aa5ed-110">You also can copy data from any supported source data store to an Oracle database.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-110">You also can copy data from any supported source data store to an Oracle database.</span></span> <span data-ttu-id="aa5ed-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-111">For a list of data stores that are supported as sources or sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="aa5ed-112">Specifically, this Oracle connector supports the following versions of an Oracle database.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-112">Specifically, this Oracle connector supports the following versions of an Oracle database.</span></span> <span data-ttu-id="aa5ed-113">It also supports Basic or OID authentications:</span><span class="sxs-lookup"><span data-stu-id="aa5ed-113">It also supports Basic or OID authentications:</span></span>

- <span data-ttu-id="aa5ed-114">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-114">Oracle 12c R1 (12.1)</span></span>
- <span data-ttu-id="aa5ed-115">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-115">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
- <span data-ttu-id="aa5ed-116">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-116">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
- <span data-ttu-id="aa5ed-117">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-117">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
- <span data-ttu-id="aa5ed-118">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-118">Oracle 8i R3 (8.1.7)</span></span>

> [!Note]
> Oracle proxy server is not supported.

## <a name="prerequisites"></a><span data-ttu-id="aa5ed-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa5ed-120">Prerequisites</span></span>

<span data-ttu-id="aa5ed-121">To copy data from and to an Oracle database that isn't publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-121">To copy data from and to an Oracle database that isn't publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="aa5ed-122">For more information about integration runtime, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-122">For more information about integration runtime, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md).</span></span> <span data-ttu-id="aa5ed-123">The integration runtime provides a built-in Oracle driver.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-123">The integration runtime provides a built-in Oracle driver.</span></span> <span data-ttu-id="aa5ed-124">Therefore, you don't need to manually install a driver when you copy data from and to Oracle.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-124">Therefore, you don't need to manually install a driver when you copy data from and to Oracle.</span></span>

## <a name="get-started"></a><span data-ttu-id="aa5ed-125">Get started</span><span class="sxs-lookup"><span data-stu-id="aa5ed-125">Get started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="aa5ed-126">The following sections provide details about properties that are used to define Data Factory entities specific to the Oracle connector.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-126">The following sections provide details about properties that are used to define Data Factory entities specific to the Oracle connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="aa5ed-127">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="aa5ed-127">Linked service properties</span></span>

<span data-ttu-id="aa5ed-128">The following properties are supported for the Oracle linked service.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-128">The following properties are supported for the Oracle linked service.</span></span>

| <span data-ttu-id="aa5ed-129">Property</span><span class="sxs-lookup"><span data-stu-id="aa5ed-129">Property</span></span> | <span data-ttu-id="aa5ed-130">Description</span><span class="sxs-lookup"><span data-stu-id="aa5ed-130">Description</span></span> | <span data-ttu-id="aa5ed-131">Required</span><span class="sxs-lookup"><span data-stu-id="aa5ed-131">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa5ed-132">type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-132">type</span></span> | <span data-ttu-id="aa5ed-133">The type property must be set to **Oracle**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-133">The type property must be set to **Oracle**.</span></span> | <span data-ttu-id="aa5ed-134">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-134">Yes</span></span> |
| <span data-ttu-id="aa5ed-135">connectionString</span><span class="sxs-lookup"><span data-stu-id="aa5ed-135">connectionString</span></span> | <span data-ttu-id="aa5ed-136">Specifies the information needed to connect to the Oracle Database instance.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-136">Specifies the information needed to connect to the Oracle Database instance.</span></span> <span data-ttu-id="aa5ed-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-137">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span><br><br><span data-ttu-id="aa5ed-138">**Supported connection type**: You can use **Oracle SID** or **Oracle Service Name** to identify your database:</span><span class="sxs-lookup"><span data-stu-id="aa5ed-138">**Supported connection type**: You can use **Oracle SID** or **Oracle Service Name** to identify your database:</span></span><br><span data-ttu-id="aa5ed-139">- If you use SID: `Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;`</span><span class="sxs-lookup"><span data-stu-id="aa5ed-139">- If you use SID: `Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;`</span></span><br><span data-ttu-id="aa5ed-140">- If you use Service Name: `Host=<host>;Port=<port>;ServiceName=<servicename>;User Id=<username>;Password=<password>;`</span><span class="sxs-lookup"><span data-stu-id="aa5ed-140">- If you use Service Name: `Host=<host>;Port=<port>;ServiceName=<servicename>;User Id=<username>;Password=<password>;`</span></span> | <span data-ttu-id="aa5ed-141">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-141">Yes</span></span> |
| <span data-ttu-id="aa5ed-142">connectVia</span><span class="sxs-lookup"><span data-stu-id="aa5ed-142">connectVia</span></span> | <span data-ttu-id="aa5ed-143">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-143">The [integration runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="aa5ed-144">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-144">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="aa5ed-145">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-145">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="aa5ed-146">No</span><span class="sxs-lookup"><span data-stu-id="aa5ed-146">No</span></span> |

>[!TIP]
>If you hit error saying "ORA-01025: UPI parameter out of range" and your Oracle is of version 8i, add `WireProtocolMode=1` to your connection string and try again.

<span data-ttu-id="aa5ed-148">To enable encryption on Oracle connection, you have two options:</span><span class="sxs-lookup"><span data-stu-id="aa5ed-148">To enable encryption on Oracle connection, you have two options:</span></span>

1.  <span data-ttu-id="aa5ed-149">On Oracle server side, go to Oracle Advanced Security (OAS) and configure the encryption settings, which supports Triple-DES Encryption (3DES) and Advanced Encryption Standard (AES), refer to details [here](https://docs.oracle.com/cd/E11882_01/network.112/e40393/asointro.htm#i1008759).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-149">On Oracle server side, go to Oracle Advanced Security (OAS) and configure the encryption settings, which supports Triple-DES Encryption (3DES) and Advanced Encryption Standard (AES), refer to details [here](https://docs.oracle.com/cd/E11882_01/network.112/e40393/asointro.htm#i1008759).</span></span> <span data-ttu-id="aa5ed-150">ADF Oracle connector automatically negotiates the encryption method to use the one you configure in OAS when establishing connection to Oracle.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-150">ADF Oracle connector automatically negotiates the encryption method to use the one you configure in OAS when establishing connection to Oracle.</span></span>

2.  <span data-ttu-id="aa5ed-151">On client side, you can add `EncryptionMethod=1` in the connection string.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-151">On client side, you can add `EncryptionMethod=1` in the connection string.</span></span> <span data-ttu-id="aa5ed-152">This will use SSL/TLS as the encryption method.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-152">This will use SSL/TLS as the encryption method.</span></span> <span data-ttu-id="aa5ed-153">To use this, you need to disable non-SSL encryption settings in OAS on the Oracle server side to avoid encryption conflict.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-153">To use this, you need to disable non-SSL encryption settings in OAS on the Oracle server side to avoid encryption conflict.</span></span>

<span data-ttu-id="aa5ed-154">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa5ed-154">**Example:**</span></span>

```json
{
    "name": "OracleLinkedService",
    "properties": {
        "type": "Oracle",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="aa5ed-155">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="aa5ed-155">Dataset properties</span></span>

<span data-ttu-id="aa5ed-156">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-156">For a full list of sections and properties available for defining datasets, see the [Datasets](concepts-datasets-linked-services.md) article.</span></span> <span data-ttu-id="aa5ed-157">This section provides a list of properties supported by the Oracle dataset.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-157">This section provides a list of properties supported by the Oracle dataset.</span></span>

<span data-ttu-id="aa5ed-158">To copy data from and to Oracle, set the type property of the dataset to **OracleTable**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-158">To copy data from and to Oracle, set the type property of the dataset to **OracleTable**.</span></span> <span data-ttu-id="aa5ed-159">The following properties are supported.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-159">The following properties are supported.</span></span>

| <span data-ttu-id="aa5ed-160">Property</span><span class="sxs-lookup"><span data-stu-id="aa5ed-160">Property</span></span> | <span data-ttu-id="aa5ed-161">Description</span><span class="sxs-lookup"><span data-stu-id="aa5ed-161">Description</span></span> | <span data-ttu-id="aa5ed-162">Required</span><span class="sxs-lookup"><span data-stu-id="aa5ed-162">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa5ed-163">type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-163">type</span></span> | <span data-ttu-id="aa5ed-164">The type property of the dataset must be set to **OracleTable**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-164">The type property of the dataset must be set to **OracleTable**.</span></span> | <span data-ttu-id="aa5ed-165">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-165">Yes</span></span> |
| <span data-ttu-id="aa5ed-166">tableName</span><span class="sxs-lookup"><span data-stu-id="aa5ed-166">tableName</span></span> |<span data-ttu-id="aa5ed-167">The name of the table in the Oracle database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-167">The name of the table in the Oracle database that the linked service refers to.</span></span> | <span data-ttu-id="aa5ed-168">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-168">Yes</span></span> |

<span data-ttu-id="aa5ed-169">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa5ed-169">**Example:**</span></span>

```json
{
    "name": "OracleDataset",
    "properties":
    {
        "type": "OracleTable",
        "linkedServiceName": {
            "referenceName": "<Oracle linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="aa5ed-170">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="aa5ed-170">Copy activity properties</span></span>

<span data-ttu-id="aa5ed-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-171">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="aa5ed-172">This section provides a list of properties supported by the Oracle source and sink.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-172">This section provides a list of properties supported by the Oracle source and sink.</span></span>

### <a name="oracle-as-a-source-type"></a><span data-ttu-id="aa5ed-173">Oracle as a source type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-173">Oracle as a source type</span></span>

<span data-ttu-id="aa5ed-174">To copy data from Oracle, set the source type in the copy activity to **OracleSource**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-174">To copy data from Oracle, set the source type in the copy activity to **OracleSource**.</span></span> <span data-ttu-id="aa5ed-175">The following properties are supported in the copy activity **source** section.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-175">The following properties are supported in the copy activity **source** section.</span></span>

| <span data-ttu-id="aa5ed-176">Property</span><span class="sxs-lookup"><span data-stu-id="aa5ed-176">Property</span></span> | <span data-ttu-id="aa5ed-177">Description</span><span class="sxs-lookup"><span data-stu-id="aa5ed-177">Description</span></span> | <span data-ttu-id="aa5ed-178">Required</span><span class="sxs-lookup"><span data-stu-id="aa5ed-178">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa5ed-179">type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-179">type</span></span> | <span data-ttu-id="aa5ed-180">The type property of the copy activity source must be set to **OracleSource**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-180">The type property of the copy activity source must be set to **OracleSource**.</span></span> | <span data-ttu-id="aa5ed-181">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-181">Yes</span></span> |
| <span data-ttu-id="aa5ed-182">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="aa5ed-182">oracleReaderQuery</span></span> | <span data-ttu-id="aa5ed-183">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-183">Use the custom SQL query to read data.</span></span> <span data-ttu-id="aa5ed-184">An example is `"SELECT * FROM MyTable"`.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-184">An example is `"SELECT * FROM MyTable"`.</span></span> | <span data-ttu-id="aa5ed-185">No</span><span class="sxs-lookup"><span data-stu-id="aa5ed-185">No</span></span> |

<span data-ttu-id="aa5ed-186">If you don't specify "oracleReaderQuery", the columns defined in the "structure" section of the dataset are used to construct a query (`select column1, column2 from mytable`) to run against the Oracle database.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-186">If you don't specify "oracleReaderQuery", the columns defined in the "structure" section of the dataset are used to construct a query (`select column1, column2 from mytable`) to run against the Oracle database.</span></span> <span data-ttu-id="aa5ed-187">If the dataset definition doesn't have "structure", all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-187">If the dataset definition doesn't have "structure", all columns are selected from the table.</span></span>

<span data-ttu-id="aa5ed-188">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa5ed-188">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromOracle",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Oracle input dataset name>",
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
                "type": "OracleSource",
                "oracleReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="oracle-as-a-sink-type"></a><span data-ttu-id="aa5ed-189">Oracle as a sink type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-189">Oracle as a sink type</span></span>

<span data-ttu-id="aa5ed-190">To copy data to Oracle, set the sink type in the copy activity to **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-190">To copy data to Oracle, set the sink type in the copy activity to **OracleSink**.</span></span> <span data-ttu-id="aa5ed-191">The following properties are supported in the copy activity **sink** section.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-191">The following properties are supported in the copy activity **sink** section.</span></span>

| <span data-ttu-id="aa5ed-192">Property</span><span class="sxs-lookup"><span data-stu-id="aa5ed-192">Property</span></span> | <span data-ttu-id="aa5ed-193">Description</span><span class="sxs-lookup"><span data-stu-id="aa5ed-193">Description</span></span> | <span data-ttu-id="aa5ed-194">Required</span><span class="sxs-lookup"><span data-stu-id="aa5ed-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aa5ed-195">type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-195">type</span></span> | <span data-ttu-id="aa5ed-196">The type property of the copy activity sink must be set to **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-196">The type property of the copy activity sink must be set to **OracleSink**.</span></span> | <span data-ttu-id="aa5ed-197">Yes</span><span class="sxs-lookup"><span data-stu-id="aa5ed-197">Yes</span></span> |
| <span data-ttu-id="aa5ed-198">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="aa5ed-198">writeBatchSize</span></span> | <span data-ttu-id="aa5ed-199">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-199">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span><br/><span data-ttu-id="aa5ed-200">Allowed values are Integer (number of rows).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-200">Allowed values are Integer (number of rows).</span></span> |<span data-ttu-id="aa5ed-201">No (default is 10,000)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-201">No (default is 10,000)</span></span> |
| <span data-ttu-id="aa5ed-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="aa5ed-202">writeBatchTimeout</span></span> | <span data-ttu-id="aa5ed-203">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-203">Wait time for the batch insert operation to complete before it times out.</span></span><br/><span data-ttu-id="aa5ed-204">Allowed values are Timespan.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-204">Allowed values are Timespan.</span></span> <span data-ttu-id="aa5ed-205">An example is 00:30:00 (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-205">An example is 00:30:00 (30 minutes).</span></span> | <span data-ttu-id="aa5ed-206">No</span><span class="sxs-lookup"><span data-stu-id="aa5ed-206">No</span></span> |
| <span data-ttu-id="aa5ed-207">preCopyScript</span><span class="sxs-lookup"><span data-stu-id="aa5ed-207">preCopyScript</span></span> | <span data-ttu-id="aa5ed-208">Specify a SQL query for the copy activity to execute before writing data into Oracle in each run.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-208">Specify a SQL query for the copy activity to execute before writing data into Oracle in each run.</span></span> <span data-ttu-id="aa5ed-209">You can use this property to clean up the preloaded data.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-209">You can use this property to clean up the preloaded data.</span></span> | <span data-ttu-id="aa5ed-210">No</span><span class="sxs-lookup"><span data-stu-id="aa5ed-210">No</span></span> |

<span data-ttu-id="aa5ed-211">**Example:**</span><span class="sxs-lookup"><span data-stu-id="aa5ed-211">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToOracle",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Oracle output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "OracleSink"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-oracle"></a><span data-ttu-id="aa5ed-212">Data type mapping for Oracle</span><span class="sxs-lookup"><span data-stu-id="aa5ed-212">Data type mapping for Oracle</span></span>

<span data-ttu-id="aa5ed-213">When you copy data from and to Oracle, the following mappings are used from Oracle data types to Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="aa5ed-213">When you copy data from and to Oracle, the following mappings are used from Oracle data types to Data Factory interim data types.</span></span> <span data-ttu-id="aa5ed-214">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-214">To learn about how the copy activity maps the source schema and data type to the sink, see [Schema and data type mappings](copy-activity-schema-and-type-mapping.md).</span></span>

| <span data-ttu-id="aa5ed-215">Oracle data type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-215">Oracle data type</span></span> | <span data-ttu-id="aa5ed-216">Data Factory interim data type</span><span class="sxs-lookup"><span data-stu-id="aa5ed-216">Data Factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="aa5ed-217">BFILE</span><span class="sxs-lookup"><span data-stu-id="aa5ed-217">BFILE</span></span> |<span data-ttu-id="aa5ed-218">Byte[]</span><span class="sxs-lookup"><span data-stu-id="aa5ed-218">Byte[]</span></span> |
| <span data-ttu-id="aa5ed-219">BLOB</span><span class="sxs-lookup"><span data-stu-id="aa5ed-219">BLOB</span></span> |<span data-ttu-id="aa5ed-220">Byte[]</span><span class="sxs-lookup"><span data-stu-id="aa5ed-220">Byte[]</span></span><br/><span data-ttu-id="aa5ed-221">(only supported on Oracle 10g and higher)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-221">(only supported on Oracle 10g and higher)</span></span> |
| <span data-ttu-id="aa5ed-222">CHAR</span><span class="sxs-lookup"><span data-stu-id="aa5ed-222">CHAR</span></span> |<span data-ttu-id="aa5ed-223">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-223">String</span></span> |
| <span data-ttu-id="aa5ed-224">CLOB</span><span class="sxs-lookup"><span data-stu-id="aa5ed-224">CLOB</span></span> |<span data-ttu-id="aa5ed-225">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-225">String</span></span> |
| <span data-ttu-id="aa5ed-226">DATE</span><span class="sxs-lookup"><span data-stu-id="aa5ed-226">DATE</span></span> |<span data-ttu-id="aa5ed-227">DateTime</span><span class="sxs-lookup"><span data-stu-id="aa5ed-227">DateTime</span></span> |
| <span data-ttu-id="aa5ed-228">FLOAT</span><span class="sxs-lookup"><span data-stu-id="aa5ed-228">FLOAT</span></span> |<span data-ttu-id="aa5ed-229">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-229">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="aa5ed-230">INTEGER</span><span class="sxs-lookup"><span data-stu-id="aa5ed-230">INTEGER</span></span> |<span data-ttu-id="aa5ed-231">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-231">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="aa5ed-232">LONG</span><span class="sxs-lookup"><span data-stu-id="aa5ed-232">LONG</span></span> |<span data-ttu-id="aa5ed-233">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-233">String</span></span> |
| <span data-ttu-id="aa5ed-234">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="aa5ed-234">LONG RAW</span></span> |<span data-ttu-id="aa5ed-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="aa5ed-235">Byte[]</span></span> |
| <span data-ttu-id="aa5ed-236">NCHAR</span><span class="sxs-lookup"><span data-stu-id="aa5ed-236">NCHAR</span></span> |<span data-ttu-id="aa5ed-237">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-237">String</span></span> |
| <span data-ttu-id="aa5ed-238">NCLOB</span><span class="sxs-lookup"><span data-stu-id="aa5ed-238">NCLOB</span></span> |<span data-ttu-id="aa5ed-239">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-239">String</span></span> |
| <span data-ttu-id="aa5ed-240">NUMBER</span><span class="sxs-lookup"><span data-stu-id="aa5ed-240">NUMBER</span></span> |<span data-ttu-id="aa5ed-241">Decimal, String (if precision > 28)</span><span class="sxs-lookup"><span data-stu-id="aa5ed-241">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="aa5ed-242">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="aa5ed-242">NVARCHAR2</span></span> |<span data-ttu-id="aa5ed-243">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-243">String</span></span> |
| <span data-ttu-id="aa5ed-244">RAW</span><span class="sxs-lookup"><span data-stu-id="aa5ed-244">RAW</span></span> |<span data-ttu-id="aa5ed-245">Byte[]</span><span class="sxs-lookup"><span data-stu-id="aa5ed-245">Byte[]</span></span> |
| <span data-ttu-id="aa5ed-246">ROWID</span><span class="sxs-lookup"><span data-stu-id="aa5ed-246">ROWID</span></span> |<span data-ttu-id="aa5ed-247">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-247">String</span></span> |
| <span data-ttu-id="aa5ed-248">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="aa5ed-248">TIMESTAMP</span></span> |<span data-ttu-id="aa5ed-249">DateTime</span><span class="sxs-lookup"><span data-stu-id="aa5ed-249">DateTime</span></span> |
| <span data-ttu-id="aa5ed-250">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="aa5ed-250">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="aa5ed-251">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-251">String</span></span> |
| <span data-ttu-id="aa5ed-252">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="aa5ed-252">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="aa5ed-253">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-253">String</span></span> |
| <span data-ttu-id="aa5ed-254">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="aa5ed-254">UNSIGNED INTEGER</span></span> |<span data-ttu-id="aa5ed-255">Number</span><span class="sxs-lookup"><span data-stu-id="aa5ed-255">Number</span></span> |
| <span data-ttu-id="aa5ed-256">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="aa5ed-256">VARCHAR2</span></span> |<span data-ttu-id="aa5ed-257">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-257">String</span></span> |
| <span data-ttu-id="aa5ed-258">XML</span><span class="sxs-lookup"><span data-stu-id="aa5ed-258">XML</span></span> |<span data-ttu-id="aa5ed-259">String</span><span class="sxs-lookup"><span data-stu-id="aa5ed-259">String</span></span> |

> [!NOTE]
> The data types INTERVAL YEAR TO MONTH and INTERVAL DAY TO SECOND aren't supported.


## <a name="next-steps"></a><span data-ttu-id="aa5ed-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa5ed-261">Next steps</span></span>
<span data-ttu-id="aa5ed-262">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="aa5ed-262">For a list of data stores supported as sources and sinks by the copy activity in Data Factory, see [Supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
