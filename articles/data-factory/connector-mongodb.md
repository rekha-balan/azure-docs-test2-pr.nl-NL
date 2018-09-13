---
title: Copy data from MongoDB using Azure Data Factory | Microsoft Docs
description: Learn how to copy data from Mongo DB to supported sink data stores by using a copy activity in an Azure Data Factory pipeline.
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
ms.date: 06/05/2018
ms.author: jingwang
ms.openlocfilehash: debb27f49c730df4a8bef42b1f1ef9ec50f1faf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867228"
---
# <a name="copy-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="fadc1-103">Copy data from MongoDB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fadc1-103">Copy data from MongoDB using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-on-premises-mongodb-connector.md)
> * [Current version](connector-mongodb.md)

<span data-ttu-id="fadc1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="fadc1-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from a MongoDB database.</span></span> <span data-ttu-id="fadc1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="fadc1-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="fadc1-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="fadc1-108">Supported capabilities</span></span>

<span data-ttu-id="fadc1-109">You can copy data from MongoDB database to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="fadc1-109">You can copy data from MongoDB database to any supported sink data store.</span></span> <span data-ttu-id="fadc1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="fadc1-110">For a list of data stores that are supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="fadc1-111">Specifically, this MongoDB connector supports:</span><span class="sxs-lookup"><span data-stu-id="fadc1-111">Specifically, this MongoDB connector supports:</span></span>

- <span data-ttu-id="fadc1-112">MongoDB **versions 2.4, 2.6, 3.0, 3.2, 3.4 and 3.6**.</span><span class="sxs-lookup"><span data-stu-id="fadc1-112">MongoDB **versions 2.4, 2.6, 3.0, 3.2, 3.4 and 3.6**.</span></span>
- <span data-ttu-id="fadc1-113">Copying data using **Basic** or **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="fadc1-113">Copying data using **Basic** or **Anonymous** authentication.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fadc1-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fadc1-114">Prerequisites</span></span>

<span data-ttu-id="fadc1-115">To copy data from a MongoDB database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="fadc1-115">To copy data from a MongoDB database that is not publicly accessible, you need to set up a Self-hosted Integration Runtime.</span></span> <span data-ttu-id="fadc1-116">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article to learn details.</span><span class="sxs-lookup"><span data-stu-id="fadc1-116">See [Self-hosted Integration Runtime](create-self-hosted-integration-runtime.md) article to learn details.</span></span> <span data-ttu-id="fadc1-117">The Integration Runtime provides a built-in MongoDB driver, therefore you don't need to manually install any driver when copying data from MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fadc1-117">The Integration Runtime provides a built-in MongoDB driver, therefore you don't need to manually install any driver when copying data from MongoDB.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fadc1-118">Getting started</span><span class="sxs-lookup"><span data-stu-id="fadc1-118">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="fadc1-119">The following sections provide details about properties that are used to define Data Factory entities specific to MongoDB connector.</span><span class="sxs-lookup"><span data-stu-id="fadc1-119">The following sections provide details about properties that are used to define Data Factory entities specific to MongoDB connector.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fadc1-120">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="fadc1-120">Linked service properties</span></span>

<span data-ttu-id="fadc1-121">The following properties are supported for MongoDB linked service:</span><span class="sxs-lookup"><span data-stu-id="fadc1-121">The following properties are supported for MongoDB linked service:</span></span>

| <span data-ttu-id="fadc1-122">Property</span><span class="sxs-lookup"><span data-stu-id="fadc1-122">Property</span></span> | <span data-ttu-id="fadc1-123">Description</span><span class="sxs-lookup"><span data-stu-id="fadc1-123">Description</span></span> | <span data-ttu-id="fadc1-124">Required</span><span class="sxs-lookup"><span data-stu-id="fadc1-124">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fadc1-125">type</span><span class="sxs-lookup"><span data-stu-id="fadc1-125">type</span></span> |<span data-ttu-id="fadc1-126">The type property must be set to: **MongoDb**</span><span class="sxs-lookup"><span data-stu-id="fadc1-126">The type property must be set to: **MongoDb**</span></span> |<span data-ttu-id="fadc1-127">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-127">Yes</span></span> |
| <span data-ttu-id="fadc1-128">server</span><span class="sxs-lookup"><span data-stu-id="fadc1-128">server</span></span> |<span data-ttu-id="fadc1-129">IP address or host name of the MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="fadc1-129">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="fadc1-130">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-130">Yes</span></span> |
| <span data-ttu-id="fadc1-131">port</span><span class="sxs-lookup"><span data-stu-id="fadc1-131">port</span></span> |<span data-ttu-id="fadc1-132">TCP port that the MongoDB server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="fadc1-132">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="fadc1-133">No (default is 27017)</span><span class="sxs-lookup"><span data-stu-id="fadc1-133">No (default is 27017)</span></span> |
| <span data-ttu-id="fadc1-134">databaseName</span><span class="sxs-lookup"><span data-stu-id="fadc1-134">databaseName</span></span> |<span data-ttu-id="fadc1-135">Name of the MongoDB database that you want to access.</span><span class="sxs-lookup"><span data-stu-id="fadc1-135">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="fadc1-136">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-136">Yes</span></span> |
| <span data-ttu-id="fadc1-137">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fadc1-137">authenticationType</span></span> | <span data-ttu-id="fadc1-138">Type of authentication used to connect to the MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="fadc1-138">Type of authentication used to connect to the MongoDB database.</span></span><br/><span data-ttu-id="fadc1-139">Allowed values are: **Basic**, and **Anonymous**.</span><span class="sxs-lookup"><span data-stu-id="fadc1-139">Allowed values are: **Basic**, and **Anonymous**.</span></span> |<span data-ttu-id="fadc1-140">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-140">Yes</span></span> |
| <span data-ttu-id="fadc1-141">username</span><span class="sxs-lookup"><span data-stu-id="fadc1-141">username</span></span> |<span data-ttu-id="fadc1-142">User account to access MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fadc1-142">User account to access MongoDB.</span></span> |<span data-ttu-id="fadc1-143">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="fadc1-143">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="fadc1-144">password</span><span class="sxs-lookup"><span data-stu-id="fadc1-144">password</span></span> |<span data-ttu-id="fadc1-145">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="fadc1-145">Password for the user.</span></span> <span data-ttu-id="fadc1-146">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="fadc1-146">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="fadc1-147">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="fadc1-147">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="fadc1-148">authSource</span><span class="sxs-lookup"><span data-stu-id="fadc1-148">authSource</span></span> |<span data-ttu-id="fadc1-149">Name of the MongoDB database that you want to use to check your credentials for authentication.</span><span class="sxs-lookup"><span data-stu-id="fadc1-149">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="fadc1-150">No.</span><span class="sxs-lookup"><span data-stu-id="fadc1-150">No.</span></span> <span data-ttu-id="fadc1-151">For basic authentication, default is to use the admin account and the database specified using databaseName property.</span><span class="sxs-lookup"><span data-stu-id="fadc1-151">For basic authentication, default is to use the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="fadc1-152">enableSsl</span><span class="sxs-lookup"><span data-stu-id="fadc1-152">enableSsl</span></span> | <span data-ttu-id="fadc1-153">Specifies whether the connections to the server are encrypted using SSL.</span><span class="sxs-lookup"><span data-stu-id="fadc1-153">Specifies whether the connections to the server are encrypted using SSL.</span></span> <span data-ttu-id="fadc1-154">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="fadc1-154">The default value is false.</span></span>  | <span data-ttu-id="fadc1-155">No</span><span class="sxs-lookup"><span data-stu-id="fadc1-155">No</span></span> |
| <span data-ttu-id="fadc1-156">allowSelfSignedServerCert</span><span class="sxs-lookup"><span data-stu-id="fadc1-156">allowSelfSignedServerCert</span></span> | <span data-ttu-id="fadc1-157">Specifies whether to allow self-signed certificates from the server.</span><span class="sxs-lookup"><span data-stu-id="fadc1-157">Specifies whether to allow self-signed certificates from the server.</span></span> <span data-ttu-id="fadc1-158">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="fadc1-158">The default value is false.</span></span>  | <span data-ttu-id="fadc1-159">No</span><span class="sxs-lookup"><span data-stu-id="fadc1-159">No</span></span> |
| <span data-ttu-id="fadc1-160">connectVia</span><span class="sxs-lookup"><span data-stu-id="fadc1-160">connectVia</span></span> | <span data-ttu-id="fadc1-161">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="fadc1-161">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="fadc1-162">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span><span class="sxs-lookup"><span data-stu-id="fadc1-162">You can use Self-hosted Integration Runtime or Azure Integration Runtime (if your data store is publicly accessible).</span></span> <span data-ttu-id="fadc1-163">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="fadc1-163">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="fadc1-164">No</span><span class="sxs-lookup"><span data-stu-id="fadc1-164">No</span></span> |

<span data-ttu-id="fadc1-165">**Example:**</span><span class="sxs-lookup"><span data-stu-id="fadc1-165">**Example:**</span></span>

```json
{
    "name": "MongoDBLinkedService",
    "properties": {
        "type": "MongoDb",
        "typeProperties": {
            "server": "<server name>",
            "databaseName": "<database name>",
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

## <a name="dataset-properties"></a><span data-ttu-id="fadc1-166">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="fadc1-166">Dataset properties</span></span>

<span data-ttu-id="fadc1-167">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="fadc1-167">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="fadc1-168">This section provides a list of properties supported by MongoDB dataset.</span><span class="sxs-lookup"><span data-stu-id="fadc1-168">This section provides a list of properties supported by MongoDB dataset.</span></span>

<span data-ttu-id="fadc1-169">To copy data from MongoDB, set the type property of the dataset to **MongoDbCollection**.</span><span class="sxs-lookup"><span data-stu-id="fadc1-169">To copy data from MongoDB, set the type property of the dataset to **MongoDbCollection**.</span></span> <span data-ttu-id="fadc1-170">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="fadc1-170">The following properties are supported:</span></span>

| <span data-ttu-id="fadc1-171">Property</span><span class="sxs-lookup"><span data-stu-id="fadc1-171">Property</span></span> | <span data-ttu-id="fadc1-172">Description</span><span class="sxs-lookup"><span data-stu-id="fadc1-172">Description</span></span> | <span data-ttu-id="fadc1-173">Required</span><span class="sxs-lookup"><span data-stu-id="fadc1-173">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fadc1-174">type</span><span class="sxs-lookup"><span data-stu-id="fadc1-174">type</span></span> | <span data-ttu-id="fadc1-175">The type property of the dataset must be set to: **MongoDbCollection**</span><span class="sxs-lookup"><span data-stu-id="fadc1-175">The type property of the dataset must be set to: **MongoDbCollection**</span></span> | <span data-ttu-id="fadc1-176">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-176">Yes</span></span> |
| <span data-ttu-id="fadc1-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="fadc1-177">collectionName</span></span> |<span data-ttu-id="fadc1-178">Name of the collection in MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="fadc1-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="fadc1-179">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-179">Yes</span></span> |

<span data-ttu-id="fadc1-180">**Example:**</span><span class="sxs-lookup"><span data-stu-id="fadc1-180">**Example:**</span></span>

```json
{
     "name":  "MongoDbDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": {
            "referenceName": "<MongoDB linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "collectionName": "<Collection name>"
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="fadc1-181">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="fadc1-181">Copy activity properties</span></span>

<span data-ttu-id="fadc1-182">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="fadc1-182">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="fadc1-183">This section provides a list of properties supported by MongoDB source.</span><span class="sxs-lookup"><span data-stu-id="fadc1-183">This section provides a list of properties supported by MongoDB source.</span></span>

### <a name="mongodb-as-source"></a><span data-ttu-id="fadc1-184">MongoDB as source</span><span class="sxs-lookup"><span data-stu-id="fadc1-184">MongoDB as source</span></span>

<span data-ttu-id="fadc1-185">To copy data from MongoDB, set the source type in the copy activity to **MongoDbSource**.</span><span class="sxs-lookup"><span data-stu-id="fadc1-185">To copy data from MongoDB, set the source type in the copy activity to **MongoDbSource**.</span></span> <span data-ttu-id="fadc1-186">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="fadc1-186">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="fadc1-187">Property</span><span class="sxs-lookup"><span data-stu-id="fadc1-187">Property</span></span> | <span data-ttu-id="fadc1-188">Description</span><span class="sxs-lookup"><span data-stu-id="fadc1-188">Description</span></span> | <span data-ttu-id="fadc1-189">Required</span><span class="sxs-lookup"><span data-stu-id="fadc1-189">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fadc1-190">type</span><span class="sxs-lookup"><span data-stu-id="fadc1-190">type</span></span> | <span data-ttu-id="fadc1-191">The type property of the copy activity source must be set to: **MongoDbSource**</span><span class="sxs-lookup"><span data-stu-id="fadc1-191">The type property of the copy activity source must be set to: **MongoDbSource**</span></span> | <span data-ttu-id="fadc1-192">Yes</span><span class="sxs-lookup"><span data-stu-id="fadc1-192">Yes</span></span> |
| <span data-ttu-id="fadc1-193">query</span><span class="sxs-lookup"><span data-stu-id="fadc1-193">query</span></span> |<span data-ttu-id="fadc1-194">Use the custom SQL-92 query to read data.</span><span class="sxs-lookup"><span data-stu-id="fadc1-194">Use the custom SQL-92 query to read data.</span></span> <span data-ttu-id="fadc1-195">For example: select \* from MyTable.</span><span class="sxs-lookup"><span data-stu-id="fadc1-195">For example: select \* from MyTable.</span></span> |<span data-ttu-id="fadc1-196">No (if "collectionName" in dataset is specified)</span><span class="sxs-lookup"><span data-stu-id="fadc1-196">No (if "collectionName" in dataset is specified)</span></span> |

<span data-ttu-id="fadc1-197">**Example:**</span><span class="sxs-lookup"><span data-stu-id="fadc1-197">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromMongoDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MongoDB input dataset name>",
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
                "type": "MongoDbSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

> [!TIP]
> When specify the SQL query, pay attention to the DateTime format. For example: `SELECT * FROM Account WHERE LastModifiedDate >= '2018-06-01' AND LastModifiedDate < '2018-06-02'` or to use parameter `SELECT * FROM Account WHERE LastModifiedDate >= '@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}' AND LastModifiedDate < '@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'`

## <a name="schema-by-data-factory"></a><span data-ttu-id="fadc1-200">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="fadc1-200">Schema by Data Factory</span></span>

<span data-ttu-id="fadc1-201">Azure Data Factory service infers schema from a MongoDB collection by using the **latest 100 documents** in the collection.</span><span class="sxs-lookup"><span data-stu-id="fadc1-201">Azure Data Factory service infers schema from a MongoDB collection by using the **latest 100 documents** in the collection.</span></span> <span data-ttu-id="fadc1-202">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span><span class="sxs-lookup"><span data-stu-id="fadc1-202">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="data-type-mapping-for-mongodb"></a><span data-ttu-id="fadc1-203">Data type mapping for MongoDB</span><span class="sxs-lookup"><span data-stu-id="fadc1-203">Data type mapping for MongoDB</span></span>

<span data-ttu-id="fadc1-204">When copying data from MongoDB, the following mappings are used from MongoDB data types to Azure Data Factory interim data types.</span><span class="sxs-lookup"><span data-stu-id="fadc1-204">When copying data from MongoDB, the following mappings are used from MongoDB data types to Azure Data Factory interim data types.</span></span> <span data-ttu-id="fadc1-205">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span><span class="sxs-lookup"><span data-stu-id="fadc1-205">See [Schema and data type mappings](copy-activity-schema-and-type-mapping.md) to learn about how copy activity maps the source schema and data type to the sink.</span></span>

| <span data-ttu-id="fadc1-206">MongoDB data type</span><span class="sxs-lookup"><span data-stu-id="fadc1-206">MongoDB data type</span></span> | <span data-ttu-id="fadc1-207">Data factory interim data type</span><span class="sxs-lookup"><span data-stu-id="fadc1-207">Data factory interim data type</span></span> |
|:--- |:--- |
| <span data-ttu-id="fadc1-208">Binary</span><span class="sxs-lookup"><span data-stu-id="fadc1-208">Binary</span></span> |<span data-ttu-id="fadc1-209">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fadc1-209">Byte[]</span></span> |
| <span data-ttu-id="fadc1-210">Boolean</span><span class="sxs-lookup"><span data-stu-id="fadc1-210">Boolean</span></span> |<span data-ttu-id="fadc1-211">Boolean</span><span class="sxs-lookup"><span data-stu-id="fadc1-211">Boolean</span></span> |
| <span data-ttu-id="fadc1-212">Date</span><span class="sxs-lookup"><span data-stu-id="fadc1-212">Date</span></span> |<span data-ttu-id="fadc1-213">DateTime</span><span class="sxs-lookup"><span data-stu-id="fadc1-213">DateTime</span></span> |
| <span data-ttu-id="fadc1-214">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="fadc1-214">NumberDouble</span></span> |<span data-ttu-id="fadc1-215">Double</span><span class="sxs-lookup"><span data-stu-id="fadc1-215">Double</span></span> |
| <span data-ttu-id="fadc1-216">NumberInt</span><span class="sxs-lookup"><span data-stu-id="fadc1-216">NumberInt</span></span> |<span data-ttu-id="fadc1-217">Int32</span><span class="sxs-lookup"><span data-stu-id="fadc1-217">Int32</span></span> |
| <span data-ttu-id="fadc1-218">NumberLong</span><span class="sxs-lookup"><span data-stu-id="fadc1-218">NumberLong</span></span> |<span data-ttu-id="fadc1-219">Int64</span><span class="sxs-lookup"><span data-stu-id="fadc1-219">Int64</span></span> |
| <span data-ttu-id="fadc1-220">ObjectID</span><span class="sxs-lookup"><span data-stu-id="fadc1-220">ObjectID</span></span> |<span data-ttu-id="fadc1-221">String</span><span class="sxs-lookup"><span data-stu-id="fadc1-221">String</span></span> |
| <span data-ttu-id="fadc1-222">String</span><span class="sxs-lookup"><span data-stu-id="fadc1-222">String</span></span> |<span data-ttu-id="fadc1-223">String</span><span class="sxs-lookup"><span data-stu-id="fadc1-223">String</span></span> |
| <span data-ttu-id="fadc1-224">UUID</span><span class="sxs-lookup"><span data-stu-id="fadc1-224">UUID</span></span> |<span data-ttu-id="fadc1-225">Guid</span><span class="sxs-lookup"><span data-stu-id="fadc1-225">Guid</span></span> |
| <span data-ttu-id="fadc1-226">Object</span><span class="sxs-lookup"><span data-stu-id="fadc1-226">Object</span></span> |<span data-ttu-id="fadc1-227">Renormalized into flatten columns with “_" as nested separator</span><span class="sxs-lookup"><span data-stu-id="fadc1-227">Renormalized into flatten columns with “_" as nested separator</span></span> |

> [!NOTE]
> To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section.
>
> Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined.

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="fadc1-230">Support for complex types using virtual tables</span><span class="sxs-lookup"><span data-stu-id="fadc1-230">Support for complex types using virtual tables</span></span>

<span data-ttu-id="fadc1-231">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="fadc1-231">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="fadc1-232">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span><span class="sxs-lookup"><span data-stu-id="fadc1-232">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="fadc1-233">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span><span class="sxs-lookup"><span data-stu-id="fadc1-233">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="fadc1-234">A **base table**, which contains the same data as the real table except for the complex type columns.</span><span class="sxs-lookup"><span data-stu-id="fadc1-234">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="fadc1-235">The base table uses the same name as the real table that it represents.</span><span class="sxs-lookup"><span data-stu-id="fadc1-235">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="fadc1-236">A **virtual table** for each complex type column, which expands the nested data.</span><span class="sxs-lookup"><span data-stu-id="fadc1-236">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="fadc1-237">The virtual tables are named using the name of the real table, a separator “_" and the name of the array or object.</span><span class="sxs-lookup"><span data-stu-id="fadc1-237">The virtual tables are named using the name of the real table, a separator “_" and the name of the array or object.</span></span>

<span data-ttu-id="fadc1-238">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span><span class="sxs-lookup"><span data-stu-id="fadc1-238">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="fadc1-239">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="fadc1-239">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

### <a name="example"></a><span data-ttu-id="fadc1-240">Example</span><span class="sxs-lookup"><span data-stu-id="fadc1-240">Example</span></span>

<span data-ttu-id="fadc1-241">For example, ExampleTable here is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span><span class="sxs-lookup"><span data-stu-id="fadc1-241">For example, ExampleTable here is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="fadc1-242">_id</span><span class="sxs-lookup"><span data-stu-id="fadc1-242">_id</span></span> | <span data-ttu-id="fadc1-243">Customer Name</span><span class="sxs-lookup"><span data-stu-id="fadc1-243">Customer Name</span></span> | <span data-ttu-id="fadc1-244">Invoices</span><span class="sxs-lookup"><span data-stu-id="fadc1-244">Invoices</span></span> | <span data-ttu-id="fadc1-245">Service Level</span><span class="sxs-lookup"><span data-stu-id="fadc1-245">Service Level</span></span> | <span data-ttu-id="fadc1-246">Ratings</span><span class="sxs-lookup"><span data-stu-id="fadc1-246">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="fadc1-247">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-247">1111</span></span> |<span data-ttu-id="fadc1-248">ABC</span><span class="sxs-lookup"><span data-stu-id="fadc1-248">ABC</span></span> |<span data-ttu-id="fadc1-249">[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}]</span><span class="sxs-lookup"><span data-stu-id="fadc1-249">[{invoice_id:"123", item:"toaster", price:"456", discount:"0.2"}, {invoice_id:"124", item:"oven", price: "1235", discount: "0.2"}]</span></span> |<span data-ttu-id="fadc1-250">Silver</span><span class="sxs-lookup"><span data-stu-id="fadc1-250">Silver</span></span> |<span data-ttu-id="fadc1-251">[5,6]</span><span class="sxs-lookup"><span data-stu-id="fadc1-251">[5,6]</span></span> |
| <span data-ttu-id="fadc1-252">2222</span><span class="sxs-lookup"><span data-stu-id="fadc1-252">2222</span></span> |<span data-ttu-id="fadc1-253">XYZ</span><span class="sxs-lookup"><span data-stu-id="fadc1-253">XYZ</span></span> |<span data-ttu-id="fadc1-254">[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}]</span><span class="sxs-lookup"><span data-stu-id="fadc1-254">[{invoice_id:"135", item:"fridge", price: "12543", discount: "0.0"}]</span></span> |<span data-ttu-id="fadc1-255">Gold</span><span class="sxs-lookup"><span data-stu-id="fadc1-255">Gold</span></span> |<span data-ttu-id="fadc1-256">[1,2]</span><span class="sxs-lookup"><span data-stu-id="fadc1-256">[1,2]</span></span> |

<span data-ttu-id="fadc1-257">The driver would generate multiple virtual tables to represent this single table.</span><span class="sxs-lookup"><span data-stu-id="fadc1-257">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="fadc1-258">The first virtual table is the base table named “ExampleTable", shown in the example.</span><span class="sxs-lookup"><span data-stu-id="fadc1-258">The first virtual table is the base table named “ExampleTable", shown in the example.</span></span> <span data-ttu-id="fadc1-259">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span><span class="sxs-lookup"><span data-stu-id="fadc1-259">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="fadc1-260">_id</span><span class="sxs-lookup"><span data-stu-id="fadc1-260">_id</span></span> | <span data-ttu-id="fadc1-261">Customer Name</span><span class="sxs-lookup"><span data-stu-id="fadc1-261">Customer Name</span></span> | <span data-ttu-id="fadc1-262">Service Level</span><span class="sxs-lookup"><span data-stu-id="fadc1-262">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fadc1-263">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-263">1111</span></span> |<span data-ttu-id="fadc1-264">ABC</span><span class="sxs-lookup"><span data-stu-id="fadc1-264">ABC</span></span> |<span data-ttu-id="fadc1-265">Silver</span><span class="sxs-lookup"><span data-stu-id="fadc1-265">Silver</span></span> |
| <span data-ttu-id="fadc1-266">2222</span><span class="sxs-lookup"><span data-stu-id="fadc1-266">2222</span></span> |<span data-ttu-id="fadc1-267">XYZ</span><span class="sxs-lookup"><span data-stu-id="fadc1-267">XYZ</span></span> |<span data-ttu-id="fadc1-268">Gold</span><span class="sxs-lookup"><span data-stu-id="fadc1-268">Gold</span></span> |

<span data-ttu-id="fadc1-269">The following tables show the virtual tables that represent the original arrays in the example.</span><span class="sxs-lookup"><span data-stu-id="fadc1-269">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="fadc1-270">These tables contain the following:</span><span class="sxs-lookup"><span data-stu-id="fadc1-270">These tables contain the following:</span></span>

* <span data-ttu-id="fadc1-271">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span><span class="sxs-lookup"><span data-stu-id="fadc1-271">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="fadc1-272">An indication of the position of the data within the original array</span><span class="sxs-lookup"><span data-stu-id="fadc1-272">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="fadc1-273">The expanded data for each element within the array</span><span class="sxs-lookup"><span data-stu-id="fadc1-273">The expanded data for each element within the array</span></span>

<span data-ttu-id="fadc1-274">**Table “ExampleTable_Invoices":**</span><span class="sxs-lookup"><span data-stu-id="fadc1-274">**Table “ExampleTable_Invoices":**</span></span>

| <span data-ttu-id="fadc1-275">_id</span><span class="sxs-lookup"><span data-stu-id="fadc1-275">_id</span></span> | <span data-ttu-id="fadc1-276">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="fadc1-276">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="fadc1-277">invoice_id</span><span class="sxs-lookup"><span data-stu-id="fadc1-277">invoice_id</span></span> | <span data-ttu-id="fadc1-278">item</span><span class="sxs-lookup"><span data-stu-id="fadc1-278">item</span></span> | <span data-ttu-id="fadc1-279">price</span><span class="sxs-lookup"><span data-stu-id="fadc1-279">price</span></span> | <span data-ttu-id="fadc1-280">Discount</span><span class="sxs-lookup"><span data-stu-id="fadc1-280">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fadc1-281">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-281">1111</span></span> |<span data-ttu-id="fadc1-282">0</span><span class="sxs-lookup"><span data-stu-id="fadc1-282">0</span></span> |<span data-ttu-id="fadc1-283">123</span><span class="sxs-lookup"><span data-stu-id="fadc1-283">123</span></span> |<span data-ttu-id="fadc1-284">toaster</span><span class="sxs-lookup"><span data-stu-id="fadc1-284">toaster</span></span> |<span data-ttu-id="fadc1-285">456</span><span class="sxs-lookup"><span data-stu-id="fadc1-285">456</span></span> |<span data-ttu-id="fadc1-286">0.2</span><span class="sxs-lookup"><span data-stu-id="fadc1-286">0.2</span></span> |
| <span data-ttu-id="fadc1-287">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-287">1111</span></span> |<span data-ttu-id="fadc1-288">1</span><span class="sxs-lookup"><span data-stu-id="fadc1-288">1</span></span> |<span data-ttu-id="fadc1-289">124</span><span class="sxs-lookup"><span data-stu-id="fadc1-289">124</span></span> |<span data-ttu-id="fadc1-290">oven</span><span class="sxs-lookup"><span data-stu-id="fadc1-290">oven</span></span> |<span data-ttu-id="fadc1-291">1235</span><span class="sxs-lookup"><span data-stu-id="fadc1-291">1235</span></span> |<span data-ttu-id="fadc1-292">0.2</span><span class="sxs-lookup"><span data-stu-id="fadc1-292">0.2</span></span> |
| <span data-ttu-id="fadc1-293">2222</span><span class="sxs-lookup"><span data-stu-id="fadc1-293">2222</span></span> |<span data-ttu-id="fadc1-294">0</span><span class="sxs-lookup"><span data-stu-id="fadc1-294">0</span></span> |<span data-ttu-id="fadc1-295">135</span><span class="sxs-lookup"><span data-stu-id="fadc1-295">135</span></span> |<span data-ttu-id="fadc1-296">fridge</span><span class="sxs-lookup"><span data-stu-id="fadc1-296">fridge</span></span> |<span data-ttu-id="fadc1-297">12543</span><span class="sxs-lookup"><span data-stu-id="fadc1-297">12543</span></span> |<span data-ttu-id="fadc1-298">0.0</span><span class="sxs-lookup"><span data-stu-id="fadc1-298">0.0</span></span> |

<span data-ttu-id="fadc1-299">**Table “ExampleTable_Ratings":**</span><span class="sxs-lookup"><span data-stu-id="fadc1-299">**Table “ExampleTable_Ratings":**</span></span>

| <span data-ttu-id="fadc1-300">_id</span><span class="sxs-lookup"><span data-stu-id="fadc1-300">_id</span></span> | <span data-ttu-id="fadc1-301">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="fadc1-301">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="fadc1-302">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="fadc1-302">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fadc1-303">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-303">1111</span></span> |<span data-ttu-id="fadc1-304">0</span><span class="sxs-lookup"><span data-stu-id="fadc1-304">0</span></span> |<span data-ttu-id="fadc1-305">5</span><span class="sxs-lookup"><span data-stu-id="fadc1-305">5</span></span> |
| <span data-ttu-id="fadc1-306">1111</span><span class="sxs-lookup"><span data-stu-id="fadc1-306">1111</span></span> |<span data-ttu-id="fadc1-307">1</span><span class="sxs-lookup"><span data-stu-id="fadc1-307">1</span></span> |<span data-ttu-id="fadc1-308">6</span><span class="sxs-lookup"><span data-stu-id="fadc1-308">6</span></span> |
| <span data-ttu-id="fadc1-309">2222</span><span class="sxs-lookup"><span data-stu-id="fadc1-309">2222</span></span> |<span data-ttu-id="fadc1-310">0</span><span class="sxs-lookup"><span data-stu-id="fadc1-310">0</span></span> |<span data-ttu-id="fadc1-311">1</span><span class="sxs-lookup"><span data-stu-id="fadc1-311">1</span></span> |
| <span data-ttu-id="fadc1-312">2222</span><span class="sxs-lookup"><span data-stu-id="fadc1-312">2222</span></span> |<span data-ttu-id="fadc1-313">1</span><span class="sxs-lookup"><span data-stu-id="fadc1-313">1</span></span> |<span data-ttu-id="fadc1-314">2</span><span class="sxs-lookup"><span data-stu-id="fadc1-314">2</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fadc1-315">Next steps</span><span class="sxs-lookup"><span data-stu-id="fadc1-315">Next steps</span></span>
<span data-ttu-id="fadc1-316">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fadc1-316">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
