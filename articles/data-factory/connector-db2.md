---
title: Copy data from DB2 using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from DB2 to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 08/17/2018
ms.author: jingwang
ms.openlocfilehash: f9d1d2181649cf24784dc7ad11638946c9ee4406
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870043"
---
# <a name="copy-data-from-db2-by-using-azure-data-factory"></a><span data-ttu-id="f3cb4-103">Copy data from DB2 by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f3cb4-103">Copy data from DB2 by using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-onprem-db2-connector.md)
> * [Current version](connector-db2.md)

<span data-ttu-id="f3cb4-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a DB2 database.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a DB2 database.</span></span> <span data-ttu-id="f3cb4-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="f3cb4-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="f3cb4-108">Supported capabilities</span></span>

<span data-ttu-id="f3cb4-109">You can copy data from DB2 database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-109">You can copy data from DB2 database to any supported sink data store.</span></span> <span data-ttu-id="f3cb4-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="f3cb4-111">Specifically, this DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager (SQLAM) version 9, 10 and 11:</span><span class="sxs-lookup"><span data-stu-id="f3cb4-111">Specifically, this DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager (SQLAM) version 9, 10 and 11:</span></span>

* <span data-ttu-id="f3cb4-112">IBM DB2 for z/OS 11.1</span><span class="sxs-lookup"><span data-stu-id="f3cb4-112">IBM DB2 for z/OS 11.1</span></span>
* <span data-ttu-id="f3cb4-113">IBM DB2 for z/OS 10.1</span><span class="sxs-lookup"><span data-stu-id="f3cb4-113">IBM DB2 for z/OS 10.1</span></span>
* <span data-ttu-id="f3cb4-114">IBM DB2 for i 7.2</span><span class="sxs-lookup"><span data-stu-id="f3cb4-114">IBM DB2 for i 7.2</span></span>
* <span data-ttu-id="f3cb4-115">IBM DB2 for i 7.1</span><span class="sxs-lookup"><span data-stu-id="f3cb4-115">IBM DB2 for i 7.1</span></span>
* <span data-ttu-id="f3cb4-116">IBM DB2 for LUW 11</span><span class="sxs-lookup"><span data-stu-id="f3cb4-116">IBM DB2 for LUW 11</span></span>
* <span data-ttu-id="f3cb4-117">IBM DB2 for LUW 10.5</span><span class="sxs-lookup"><span data-stu-id="f3cb4-117">IBM DB2 for LUW 10.5</span></span>
* <span data-ttu-id="f3cb4-118">IBM DB2 for LUW 10.1</span><span class="sxs-lookup"><span data-stu-id="f3cb4-118">IBM DB2 for LUW 10.1</span></span>

> [!TIP]
> If you receive an error message that states "The package corresponding to an SQL statement execution request was not found. SQLSTATE=51002 SQLCODE=-805", the reason is a needed package is not created for normal user on such OS. Follow these instructions according to your DB2 server type:
> - DB2 for i (AS400): let power user create collection for the login user before using copy activity. Command: `create collection <username>`
> - DB2 for z/OS or LUW: use a high privilege account - power user or admin with package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions - to run the copy activity once, then the needed package is automatically created during copy. Afterwards, you can switch back to normal user for your subsequent copy runs.

## <a name="prerequisites"></a><span data-ttu-id="f3cb4-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f3cb4-126">Prerequisites</span></span>

<span data-ttu-id="f3cb4-127">To use copy data from a DB2 database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-127">To use copy data from a DB2 database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="f3cb4-128">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-128">To learn about Self-hosted integration runtimes, see [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article.</span></span> <span data-ttu-id="f3cb4-129">The Integration Runtime provides a built-in DB2 driver, therefore you don't need to manually install any driver when copying data from DB2.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-129">The Integration Runtime provides a built-in DB2 driver, therefore you don't need to manually install any driver when copying data from DB2.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f3cb4-130">Getting started</span><span class="sxs-lookup"><span data-stu-id="f3cb4-130">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="f3cb4-131">The following sections provide details about properties that are used to define Data Factory entities specific to DB2 connector.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-131">The following sections provide details about properties that are used to define Data Factory entities specific to DB2 connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f3cb4-132">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f3cb4-132">Linked service properties</span></span>

<span data-ttu-id="f3cb4-133">The following properties are supported for DB2 linked service:</span><span class="sxs-lookup"><span data-stu-id="f3cb4-133">The following properties are supported for DB2 linked service:</span></span>

| <span data-ttu-id="f3cb4-134">Property</span><span class="sxs-lookup"><span data-stu-id="f3cb4-134">Property</span></span> | <span data-ttu-id="f3cb4-135">Description</span><span class="sxs-lookup"><span data-stu-id="f3cb4-135">Description</span></span> | <span data-ttu-id="f3cb4-136">Required</span><span class="sxs-lookup"><span data-stu-id="f3cb4-136">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f3cb4-137">type</span><span class="sxs-lookup"><span data-stu-id="f3cb4-137">type</span></span> | <span data-ttu-id="f3cb4-138">The type property must be set to: **Db2**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-138">The type property must be set to: **Db2**</span></span> | <span data-ttu-id="f3cb4-139">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-139">Yes</span></span> |
| <span data-ttu-id="f3cb4-140">server</span><span class="sxs-lookup"><span data-stu-id="f3cb4-140">server</span></span> |<span data-ttu-id="f3cb4-141">Name of the DB2 server.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-141">Name of the DB2 server.</span></span> <span data-ttu-id="f3cb4-142">You can specify the port number following the server name delimited by colon e.g. `server:port`.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-142">You can specify the port number following the server name delimited by colon e.g. `server:port`.</span></span> |<span data-ttu-id="f3cb4-143">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-143">Yes</span></span> |
| <span data-ttu-id="f3cb4-144">database</span><span class="sxs-lookup"><span data-stu-id="f3cb4-144">database</span></span> |<span data-ttu-id="f3cb4-145">Name of the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-145">Name of the DB2 database.</span></span> |<span data-ttu-id="f3cb4-146">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-146">Yes</span></span> |
| <span data-ttu-id="f3cb4-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f3cb4-147">authenticationType</span></span> |<span data-ttu-id="f3cb4-148">Type of authentication used to connect to the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-148">Type of authentication used to connect to the DB2 database.</span></span><br/><span data-ttu-id="f3cb4-149">Allowed value is: **Basic**.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-149">Allowed value is: **Basic**.</span></span> |<span data-ttu-id="f3cb4-150">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-150">Yes</span></span> |
| <span data-ttu-id="f3cb4-151">username</span><span class="sxs-lookup"><span data-stu-id="f3cb4-151">username</span></span> |<span data-ttu-id="f3cb4-152">Specify user name to connect to the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-152">Specify user name to connect to the DB2 database.</span></span> |<span data-ttu-id="f3cb4-153">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-153">Yes</span></span> |
| <span data-ttu-id="f3cb4-154">password</span><span class="sxs-lookup"><span data-stu-id="f3cb4-154">password</span></span> |<span data-ttu-id="f3cb4-155">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-155">Specify password for the user account you specified for the username.</span></span> <span data-ttu-id="f3cb4-156">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f3cb4-156">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="f3cb4-157">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-157">Yes</span></span> |
| <span data-ttu-id="f3cb4-158">connectVia</span><span class="sxs-lookup"><span data-stu-id="f3cb4-158">connectVia</span></span> | <span data-ttu-id="f3cb4-159">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-159">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="f3cb4-160">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="f3cb4-160">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="f3cb4-161">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-161">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="f3cb4-162">No</span><span class="sxs-lookup"><span data-stu-id="f3cb4-162">No</span></span> |

<span data-ttu-id="f3cb4-163">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-163">**Example:**</span></span>

```json
{
    "name": "Db2LinkedService",
    "properties": {
        "type": "Db2",
        "typeProperties": {
            "server": "<servername:port>",
            "database": "<dbname>",
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

## <a name="dataset-properties"></a><span data-ttu-id="f3cb4-164">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f3cb4-164">Dataset properties</span></span>

<span data-ttu-id="f3cb4-165">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-165">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="f3cb4-166">This section provides a list of properties supported by DB2 dataset.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-166">This section provides a list of properties supported by DB2 dataset.</span></span>

<span data-ttu-id="f3cb4-167">To copy data from DB2, set the type property of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-167">To copy data from DB2, set the type property of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="f3cb4-168">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="f3cb4-168">The following properties are supported:</span></span>

| <span data-ttu-id="f3cb4-169">Property</span><span class="sxs-lookup"><span data-stu-id="f3cb4-169">Property</span></span> | <span data-ttu-id="f3cb4-170">Description</span><span class="sxs-lookup"><span data-stu-id="f3cb4-170">Description</span></span> | <span data-ttu-id="f3cb4-171">Required</span><span class="sxs-lookup"><span data-stu-id="f3cb4-171">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f3cb4-172">type</span><span class="sxs-lookup"><span data-stu-id="f3cb4-172">type</span></span> | <span data-ttu-id="f3cb4-173">The type property of the dataset must be set to: **RelationalTable**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-173">The type property of the dataset must be set to: **RelationalTable**</span></span> | <span data-ttu-id="f3cb4-174">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-174">Yes</span></span> |
| <span data-ttu-id="f3cb4-175">tableName</span><span class="sxs-lookup"><span data-stu-id="f3cb4-175">tableName</span></span> | <span data-ttu-id="f3cb4-176">Name of the table in the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-176">Name of the table in the DB2 database.</span></span> | <span data-ttu-id="f3cb4-177">No (if "query" in activity source is specified)</span><span class="sxs-lookup"><span data-stu-id="f3cb4-177">No (if "query" in activity source is specified)</span></span> |

<span data-ttu-id="f3cb4-178">**Example**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-178">**Example**</span></span>

```json
{
    "name": "DB2Dataset",
    "properties":
    {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<DB2 linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="f3cb4-179">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f3cb4-179">Copy activity properties</span></span>

<span data-ttu-id="f3cb4-180">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-180">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="f3cb4-181">This section provides a list of properties supported by DB2 source.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-181">This section provides a list of properties supported by DB2 source.</span></span>

### <a name="db2-as-source"></a><span data-ttu-id="f3cb4-182">DB2 as source</span><span class="sxs-lookup"><span data-stu-id="f3cb4-182">DB2 as source</span></span>

<span data-ttu-id="f3cb4-183">To copy data from DB2, set the source type in the copy activity to **RelationalSource**.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-183">To copy data from DB2, set the source type in the copy activity to **RelationalSource**.</span></span> <span data-ttu-id="f3cb4-184">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="f3cb4-184">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="f3cb4-185">Property</span><span class="sxs-lookup"><span data-stu-id="f3cb4-185">Property</span></span> | <span data-ttu-id="f3cb4-186">Description</span><span class="sxs-lookup"><span data-stu-id="f3cb4-186">Description</span></span> | <span data-ttu-id="f3cb4-187">Required</span><span class="sxs-lookup"><span data-stu-id="f3cb4-187">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f3cb4-188">type</span><span class="sxs-lookup"><span data-stu-id="f3cb4-188">type</span></span> | <span data-ttu-id="f3cb4-189">The type property of the copy activity source must be set to: **RelationalSource**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-189">The type property of the copy activity source must be set to: **RelationalSource**</span></span> | <span data-ttu-id="f3cb4-190">Yes</span><span class="sxs-lookup"><span data-stu-id="f3cb4-190">Yes</span></span> |
| <span data-ttu-id="f3cb4-191">query</span><span class="sxs-lookup"><span data-stu-id="f3cb4-191">query</span></span> | <span data-ttu-id="f3cb4-192">Use the custom SQL query to read data.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-192">Use the custom SQL query to read data.</span></span> <span data-ttu-id="f3cb4-193">For example: `"query": "SELECT * FROM \"DB2ADMIN\".\"Customers\""`.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-193">For example: `"query": "SELECT * FROM \"DB2ADMIN\".\"Customers\""`.</span></span> | <span data-ttu-id="f3cb4-194">No (if "tableName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="f3cb4-194">No (if "tableName" in dataset is specified)</span></span> |

<span data-ttu-id="f3cb4-195">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f3cb4-195">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromDB2",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<DB2 input dataset name>",
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
                "query": "SELECT * FROM \"DB2ADMIN\".\"Customers\""
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-db2"></a><span data-ttu-id="f3cb4-196">Data type mapping for DB2</span><span class="sxs-lookup"><span data-stu-id="f3cb4-196">Data type mapping for DB2</span></span>

<span data-ttu-id="f3cb4-197">When copying data from DB2, the following mappings are used from DB2 data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-197">When copying data from DB2, the following mappings are used from DB2 data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="f3cb4-198">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="f3cb4-198">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="f3cb4-199">DB2 Database type</span><span class="sxs-lookup"><span data-stu-id="f3cb4-199">DB2 Database type</span></span> | <span data-ttu-id="f3cb4-200">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="f3cb4-200">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="f3cb4-201">BigInt</span><span class="sxs-lookup"><span data-stu-id="f3cb4-201">BigInt</span></span> |<span data-ttu-id="f3cb4-202">Int64</span><span class="sxs-lookup"><span data-stu-id="f3cb4-202">Int64</span></span> |
| <span data-ttu-id="f3cb4-203">Binary</span><span class="sxs-lookup"><span data-stu-id="f3cb4-203">Binary</span></span> |<span data-ttu-id="f3cb4-204">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3cb4-204">Byte[]</span></span> |
| <span data-ttu-id="f3cb4-205">Blob</span><span class="sxs-lookup"><span data-stu-id="f3cb4-205">Blob</span></span> |<span data-ttu-id="f3cb4-206">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3cb4-206">Byte[]</span></span> |
| <span data-ttu-id="f3cb4-207">Char</span><span class="sxs-lookup"><span data-stu-id="f3cb4-207">Char</span></span> |<span data-ttu-id="f3cb4-208">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-208">String</span></span> |
| <span data-ttu-id="f3cb4-209">Clob</span><span class="sxs-lookup"><span data-stu-id="f3cb4-209">Clob</span></span> |<span data-ttu-id="f3cb4-210">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-210">String</span></span> |
| <span data-ttu-id="f3cb4-211">Date</span><span class="sxs-lookup"><span data-stu-id="f3cb4-211">Date</span></span> |<span data-ttu-id="f3cb4-212">Datetime</span><span class="sxs-lookup"><span data-stu-id="f3cb4-212">Datetime</span></span> |
| <span data-ttu-id="f3cb4-213">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="f3cb4-213">DB2DynArray</span></span> |<span data-ttu-id="f3cb4-214">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-214">String</span></span> |
| <span data-ttu-id="f3cb4-215">DbClob</span><span class="sxs-lookup"><span data-stu-id="f3cb4-215">DbClob</span></span> |<span data-ttu-id="f3cb4-216">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-216">String</span></span> |
| <span data-ttu-id="f3cb4-217">Decimal</span><span class="sxs-lookup"><span data-stu-id="f3cb4-217">Decimal</span></span> |<span data-ttu-id="f3cb4-218">Decimal</span><span class="sxs-lookup"><span data-stu-id="f3cb4-218">Decimal</span></span> |
| <span data-ttu-id="f3cb4-219">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="f3cb4-219">DecimalFloat</span></span> |<span data-ttu-id="f3cb4-220">Decimal</span><span class="sxs-lookup"><span data-stu-id="f3cb4-220">Decimal</span></span> |
| <span data-ttu-id="f3cb4-221">Double</span><span class="sxs-lookup"><span data-stu-id="f3cb4-221">Double</span></span> |<span data-ttu-id="f3cb4-222">Double</span><span class="sxs-lookup"><span data-stu-id="f3cb4-222">Double</span></span> |
| <span data-ttu-id="f3cb4-223">Float</span><span class="sxs-lookup"><span data-stu-id="f3cb4-223">Float</span></span> |<span data-ttu-id="f3cb4-224">Double</span><span class="sxs-lookup"><span data-stu-id="f3cb4-224">Double</span></span> |
| <span data-ttu-id="f3cb4-225">Graphic</span><span class="sxs-lookup"><span data-stu-id="f3cb4-225">Graphic</span></span> |<span data-ttu-id="f3cb4-226">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-226">String</span></span> |
| <span data-ttu-id="f3cb4-227">Integer</span><span class="sxs-lookup"><span data-stu-id="f3cb4-227">Integer</span></span> |<span data-ttu-id="f3cb4-228">Int32</span><span class="sxs-lookup"><span data-stu-id="f3cb4-228">Int32</span></span> |
| <span data-ttu-id="f3cb4-229">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="f3cb4-229">LongVarBinary</span></span> |<span data-ttu-id="f3cb4-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3cb4-230">Byte[]</span></span> |
| <span data-ttu-id="f3cb4-231">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="f3cb4-231">LongVarChar</span></span> |<span data-ttu-id="f3cb4-232">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-232">String</span></span> |
| <span data-ttu-id="f3cb4-233">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="f3cb4-233">LongVarGraphic</span></span> |<span data-ttu-id="f3cb4-234">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-234">String</span></span> |
| <span data-ttu-id="f3cb4-235">Numeric</span><span class="sxs-lookup"><span data-stu-id="f3cb4-235">Numeric</span></span> |<span data-ttu-id="f3cb4-236">Decimal</span><span class="sxs-lookup"><span data-stu-id="f3cb4-236">Decimal</span></span> |
| <span data-ttu-id="f3cb4-237">Real</span><span class="sxs-lookup"><span data-stu-id="f3cb4-237">Real</span></span> |<span data-ttu-id="f3cb4-238">Single</span><span class="sxs-lookup"><span data-stu-id="f3cb4-238">Single</span></span> |
| <span data-ttu-id="f3cb4-239">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f3cb4-239">SmallInt</span></span> |<span data-ttu-id="f3cb4-240">Int16</span><span class="sxs-lookup"><span data-stu-id="f3cb4-240">Int16</span></span> |
| <span data-ttu-id="f3cb4-241">Time</span><span class="sxs-lookup"><span data-stu-id="f3cb4-241">Time</span></span> |<span data-ttu-id="f3cb4-242">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f3cb4-242">TimeSpan</span></span> |
| <span data-ttu-id="f3cb4-243">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f3cb4-243">Timestamp</span></span> |<span data-ttu-id="f3cb4-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="f3cb4-244">DateTime</span></span> |
| <span data-ttu-id="f3cb4-245">VarBinary</span><span class="sxs-lookup"><span data-stu-id="f3cb4-245">VarBinary</span></span> |<span data-ttu-id="f3cb4-246">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3cb4-246">Byte[]</span></span> |
| <span data-ttu-id="f3cb4-247">VarChar</span><span class="sxs-lookup"><span data-stu-id="f3cb4-247">VarChar</span></span> |<span data-ttu-id="f3cb4-248">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-248">String</span></span> |
| <span data-ttu-id="f3cb4-249">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="f3cb4-249">VarGraphic</span></span> |<span data-ttu-id="f3cb4-250">String</span><span class="sxs-lookup"><span data-stu-id="f3cb4-250">String</span></span> |
| <span data-ttu-id="f3cb4-251">Xml</span><span class="sxs-lookup"><span data-stu-id="f3cb4-251">Xml</span></span> |<span data-ttu-id="f3cb4-252">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f3cb4-252">Byte[]</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f3cb4-253">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3cb4-253">Next steps</span></span>
<span data-ttu-id="f3cb4-254">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f3cb4-254">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
