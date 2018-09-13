---
title: Copy data to/from Azure Cosmos DB using Data Factory | Microsoft Docs
description: Learn how to copy data from supported source data stores to Azure Cosmos DB (or) from Cosmos DB to supported sink stores using Data Factory.
services: data-factory, cosmosdb
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/28/2018
ms.author: jingwang
ms.openlocfilehash: 1afd64fbd7019164f0e1f5c850f2dcd8250cdbfc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968771"
---
# <a name="copy-data-to-or-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="f839d-103">Copy data to or from Azure Cosmos DB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f839d-103">Copy data to or from Azure Cosmos DB using Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-azure-documentdb-connector.md)
> * [Current version](connector-azure-cosmos-db.md)

<span data-ttu-id="f839d-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to Azure Cosmos DB (SQL API).</span><span class="sxs-lookup"><span data-stu-id="f839d-106">This article outlines how to use the Copy Activity in Azure Data Factory to copy data from and to Azure Cosmos DB (SQL API).</span></span> <span data-ttu-id="f839d-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span><span class="sxs-lookup"><span data-stu-id="f839d-107">It builds on the [copy activity overview](copy-activity-overview.md) article that presents a general overview of copy activity.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="f839d-108">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="f839d-108">Supported capabilities</span></span>

<span data-ttu-id="f839d-109">You can copy data from Azure Cosmos DB to any supported sink data store, or copy data from any supported source data store to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f839d-109">You can copy data from Azure Cosmos DB to any supported sink data store, or copy data from any supported source data store to Azure Cosmos DB.</span></span> <span data-ttu-id="f839d-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="f839d-110">For a list of data stores supported as sources/sinks by the copy activity, see the [Supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="f839d-111">Specifically, this Azure Cosmos DB connector supports:</span><span class="sxs-lookup"><span data-stu-id="f839d-111">Specifically, this Azure Cosmos DB connector supports:</span></span>

- <span data-ttu-id="f839d-112">Cosmos DB [SQL API](https://docs.microsoft.com/azure/cosmos-db/documentdb-introduction).</span><span class="sxs-lookup"><span data-stu-id="f839d-112">Cosmos DB [SQL API](https://docs.microsoft.com/azure/cosmos-db/documentdb-introduction).</span></span>
- <span data-ttu-id="f839d-113">Importing/exporting JSON documents as-is, or copying data from/to tabular dataset e.g. SQL database, CSV files, etc. To copy documents as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="f839d-113">Importing/exporting JSON documents as-is, or copying data from/to tabular dataset e.g. SQL database, CSV files, etc. To copy documents as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

<span data-ttu-id="f839d-114">Data Factory integrates with [Cosmos DB bulk executor library](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) to provide the best performance writing into Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f839d-114">Data Factory integrates with [Cosmos DB bulk executor library](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) to provide the best performance writing into Cosmos DB.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f839d-115">Getting started</span><span class="sxs-lookup"><span data-stu-id="f839d-115">Getting started</span></span>

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

<span data-ttu-id="f839d-116">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f839d-116">The following sections provide details about properties that are used to define Data Factory entities specific to Azure Cosmos DB.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f839d-117">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="f839d-117">Linked service properties</span></span>

<span data-ttu-id="f839d-118">The following properties are supported for Azure Cosmos DB linked service:</span><span class="sxs-lookup"><span data-stu-id="f839d-118">The following properties are supported for Azure Cosmos DB linked service:</span></span>

| <span data-ttu-id="f839d-119">Property</span><span class="sxs-lookup"><span data-stu-id="f839d-119">Property</span></span> | <span data-ttu-id="f839d-120">Description</span><span class="sxs-lookup"><span data-stu-id="f839d-120">Description</span></span> | <span data-ttu-id="f839d-121">Required</span><span class="sxs-lookup"><span data-stu-id="f839d-121">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f839d-122">type</span><span class="sxs-lookup"><span data-stu-id="f839d-122">type</span></span> | <span data-ttu-id="f839d-123">The type property must be set to: **CosmosDb**.</span><span class="sxs-lookup"><span data-stu-id="f839d-123">The type property must be set to: **CosmosDb**.</span></span> | <span data-ttu-id="f839d-124">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-124">Yes</span></span> |
| <span data-ttu-id="f839d-125">connectionString</span><span class="sxs-lookup"><span data-stu-id="f839d-125">connectionString</span></span> |<span data-ttu-id="f839d-126">Specify information needed to connect to Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="f839d-126">Specify information needed to connect to Azure Cosmos DB database.</span></span> <span data-ttu-id="f839d-127">Note you need to specify database info in the connection string as below sample.</span><span class="sxs-lookup"><span data-stu-id="f839d-127">Note you need to specify database info in the connection string as below sample.</span></span> <span data-ttu-id="f839d-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f839d-128">Mark this field as a SecureString to store it securely in Data Factory, or [reference a secret stored in Azure Key Vault](store-credentials-in-key-vault.md).</span></span> |<span data-ttu-id="f839d-129">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-129">Yes</span></span> |
| <span data-ttu-id="f839d-130">connectVia</span><span class="sxs-lookup"><span data-stu-id="f839d-130">connectVia</span></span> | <span data-ttu-id="f839d-131">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span><span class="sxs-lookup"><span data-stu-id="f839d-131">The [Integration Runtime](concepts-integration-runtime.md) to be used to connect to the data store.</span></span> <span data-ttu-id="f839d-132">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span><span class="sxs-lookup"><span data-stu-id="f839d-132">You can use Azure Integration Runtime or Self-hosted Integration Runtime (if your data store is located in private network).</span></span> <span data-ttu-id="f839d-133">If not specified, it uses the default Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="f839d-133">If not specified, it uses the default Azure Integration Runtime.</span></span> |<span data-ttu-id="f839d-134">No</span><span class="sxs-lookup"><span data-stu-id="f839d-134">No</span></span> |

<span data-ttu-id="f839d-135">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f839d-135">**Example:**</span></span>

```json
{
    "name": "CosmosDbLinkedService",
    "properties": {
        "type": "CosmosDb",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f839d-136">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="f839d-136">Dataset properties</span></span>

<span data-ttu-id="f839d-137">For a full list of sections and properties available for defining datasets, see the datasets article.</span><span class="sxs-lookup"><span data-stu-id="f839d-137">For a full list of sections and properties available for defining datasets, see the datasets article.</span></span> <span data-ttu-id="f839d-138">This section provides a list of properties supported by Azure Cosmos DB dataset.</span><span class="sxs-lookup"><span data-stu-id="f839d-138">This section provides a list of properties supported by Azure Cosmos DB dataset.</span></span>

<span data-ttu-id="f839d-139">To copy data from/to Azure Cosmos DB, set the type property of the dataset to **DocumentDbCollection**.</span><span class="sxs-lookup"><span data-stu-id="f839d-139">To copy data from/to Azure Cosmos DB, set the type property of the dataset to **DocumentDbCollection**.</span></span> <span data-ttu-id="f839d-140">The following properties are supported:</span><span class="sxs-lookup"><span data-stu-id="f839d-140">The following properties are supported:</span></span>

| <span data-ttu-id="f839d-141">Property</span><span class="sxs-lookup"><span data-stu-id="f839d-141">Property</span></span> | <span data-ttu-id="f839d-142">Description</span><span class="sxs-lookup"><span data-stu-id="f839d-142">Description</span></span> | <span data-ttu-id="f839d-143">Required</span><span class="sxs-lookup"><span data-stu-id="f839d-143">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f839d-144">type</span><span class="sxs-lookup"><span data-stu-id="f839d-144">type</span></span> | <span data-ttu-id="f839d-145">The type property of the dataset must be set to: **DocumentDbCollection**</span><span class="sxs-lookup"><span data-stu-id="f839d-145">The type property of the dataset must be set to: **DocumentDbCollection**</span></span> |<span data-ttu-id="f839d-146">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-146">Yes</span></span> |
| <span data-ttu-id="f839d-147">collectionName</span><span class="sxs-lookup"><span data-stu-id="f839d-147">collectionName</span></span> |<span data-ttu-id="f839d-148">Name of the Cosmos DB document collection.</span><span class="sxs-lookup"><span data-stu-id="f839d-148">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="f839d-149">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-149">Yes</span></span> |

<span data-ttu-id="f839d-150">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f839d-150">**Example:**</span></span>

```json
{
    "name": "CosmosDbDataset",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName":{
            "referenceName": "<Azure Cosmos DB linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "collectionName": "<collection name>"
        }
    }
}
```

### <a name="schema-by-data-factory"></a><span data-ttu-id="f839d-151">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="f839d-151">Schema by Data Factory</span></span>

<span data-ttu-id="f839d-152">For schema-free data stores such as Azure Cosmos DB, copy activity infers the schema in one of the following ways.</span><span class="sxs-lookup"><span data-stu-id="f839d-152">For schema-free data stores such as Azure Cosmos DB, copy activity infers the schema in one of the following ways.</span></span> <span data-ttu-id="f839d-153">Therefore, unless you want to [import/export JSON documents as-is](#importexport-json-documents), the best practice is to specify the structure of data in the **structure** section.</span><span class="sxs-lookup"><span data-stu-id="f839d-153">Therefore, unless you want to [import/export JSON documents as-is](#importexport-json-documents), the best practice is to specify the structure of data in the **structure** section.</span></span>

<span data-ttu-id="f839d-154">\*.</span><span class="sxs-lookup"><span data-stu-id="f839d-154">\*.</span></span> <span data-ttu-id="f839d-155">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="f839d-155">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="f839d-156">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span><span class="sxs-lookup"><span data-stu-id="f839d-156">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
<span data-ttu-id="f839d-157">\*.</span><span class="sxs-lookup"><span data-stu-id="f839d-157">\*.</span></span> <span data-ttu-id="f839d-158">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="f839d-158">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="f839d-159">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span><span class="sxs-lookup"><span data-stu-id="f839d-159">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f839d-160">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="f839d-160">Copy activity properties</span></span>

<span data-ttu-id="f839d-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="f839d-161">For a full list of sections and properties available for defining activities, see the [Pipelines](concepts-pipelines-activities.md) article.</span></span> <span data-ttu-id="f839d-162">This section provides a list of properties supported by Azure Cosmos DB source and sink.</span><span class="sxs-lookup"><span data-stu-id="f839d-162">This section provides a list of properties supported by Azure Cosmos DB source and sink.</span></span>

### <a name="azure-cosmos-db-as-source"></a><span data-ttu-id="f839d-163">Azure Cosmos DB as source</span><span class="sxs-lookup"><span data-stu-id="f839d-163">Azure Cosmos DB as source</span></span>

<span data-ttu-id="f839d-164">To copy data from Azure Cosmos DB, set the source type in the copy activity to **DocumentDbCollectionSource**.</span><span class="sxs-lookup"><span data-stu-id="f839d-164">To copy data from Azure Cosmos DB, set the source type in the copy activity to **DocumentDbCollectionSource**.</span></span> <span data-ttu-id="f839d-165">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="f839d-165">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="f839d-166">Property</span><span class="sxs-lookup"><span data-stu-id="f839d-166">Property</span></span> | <span data-ttu-id="f839d-167">Description</span><span class="sxs-lookup"><span data-stu-id="f839d-167">Description</span></span> | <span data-ttu-id="f839d-168">Required</span><span class="sxs-lookup"><span data-stu-id="f839d-168">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f839d-169">type</span><span class="sxs-lookup"><span data-stu-id="f839d-169">type</span></span> | <span data-ttu-id="f839d-170">The type property of the copy activity source must be set to: **DocumentDbCollectionSource**</span><span class="sxs-lookup"><span data-stu-id="f839d-170">The type property of the copy activity source must be set to: **DocumentDbCollectionSource**</span></span> |<span data-ttu-id="f839d-171">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-171">Yes</span></span> |
| <span data-ttu-id="f839d-172">query</span><span class="sxs-lookup"><span data-stu-id="f839d-172">query</span></span> |<span data-ttu-id="f839d-173">Specify the Cosmos DB query to read data.</span><span class="sxs-lookup"><span data-stu-id="f839d-173">Specify the Cosmos DB query to read data.</span></span><br/><br/><span data-ttu-id="f839d-174">Example: `SELECT c.BusinessEntityID, c.Name.First AS FirstName, c.Name.Middle AS MiddleName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="f839d-174">Example: `SELECT c.BusinessEntityID, c.Name.First AS FirstName, c.Name.Middle AS MiddleName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="f839d-175">No</span><span class="sxs-lookup"><span data-stu-id="f839d-175">No</span></span> <br/><br/><span data-ttu-id="f839d-176">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="f839d-176">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="f839d-177">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="f839d-177">nestingSeparator</span></span> |<span data-ttu-id="f839d-178">Special character to indicate that the document is nested and how to flattern the result set.</span><span class="sxs-lookup"><span data-stu-id="f839d-178">Special character to indicate that the document is nested and how to flattern the result set.</span></span><br/><br/><span data-ttu-id="f839d-179">For example, if a Cosmos DB query returns a nested result `"Name": {"First": "John"}`, copy activity will identify column name as "Name.First" with value "John" when the nestedSeparator is dot.</span><span class="sxs-lookup"><span data-stu-id="f839d-179">For example, if a Cosmos DB query returns a nested result `"Name": {"First": "John"}`, copy activity will identify column name as "Name.First" with value "John" when the nestedSeparator is dot.</span></span> |<span data-ttu-id="f839d-180">No (default is dot `.`)</span><span class="sxs-lookup"><span data-stu-id="f839d-180">No (default is dot `.`)</span></span> |

<span data-ttu-id="f839d-181">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f839d-181">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyFromCosmosDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Document DB input dataset name>",
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
                "type": "DocumentDbCollectionSource",
                "query": "SELECT c.BusinessEntityID, c.Name.First AS FirstName, c.Name.Middle AS MiddleName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\""
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="azure-cosmos-db-as-sink"></a><span data-ttu-id="f839d-182">Azure Cosmos DB as sink</span><span class="sxs-lookup"><span data-stu-id="f839d-182">Azure Cosmos DB as sink</span></span>

<span data-ttu-id="f839d-183">To copy data to Azure Cosmos DB, set the sink type in the copy activity to **DocumentDbCollectionSink**.</span><span class="sxs-lookup"><span data-stu-id="f839d-183">To copy data to Azure Cosmos DB, set the sink type in the copy activity to **DocumentDbCollectionSink**.</span></span> <span data-ttu-id="f839d-184">The following properties are supported in the copy activity **source** section:</span><span class="sxs-lookup"><span data-stu-id="f839d-184">The following properties are supported in the copy activity **source** section:</span></span>

| <span data-ttu-id="f839d-185">Property</span><span class="sxs-lookup"><span data-stu-id="f839d-185">Property</span></span> | <span data-ttu-id="f839d-186">Description</span><span class="sxs-lookup"><span data-stu-id="f839d-186">Description</span></span> | <span data-ttu-id="f839d-187">Required</span><span class="sxs-lookup"><span data-stu-id="f839d-187">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f839d-188">type</span><span class="sxs-lookup"><span data-stu-id="f839d-188">type</span></span> | <span data-ttu-id="f839d-189">The type property of the copy activity sink must be set to: **DocumentDbCollectionSink**</span><span class="sxs-lookup"><span data-stu-id="f839d-189">The type property of the copy activity sink must be set to: **DocumentDbCollectionSink**</span></span> |<span data-ttu-id="f839d-190">Yes</span><span class="sxs-lookup"><span data-stu-id="f839d-190">Yes</span></span> |
| <span data-ttu-id="f839d-191">writeBehavior</span><span class="sxs-lookup"><span data-stu-id="f839d-191">writeBehavior</span></span> |<span data-ttu-id="f839d-192">Describe how to write data into Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f839d-192">Describe how to write data into Cosmos DB.</span></span> <span data-ttu-id="f839d-193">Allowed values are: `insert` and `upsert`.</span><span class="sxs-lookup"><span data-stu-id="f839d-193">Allowed values are: `insert` and `upsert`.</span></span><br/><span data-ttu-id="f839d-194">The behavior of **upsert** is to replace the document if an document of the same id already exist; otherwise insert it.</span><span class="sxs-lookup"><span data-stu-id="f839d-194">The behavior of **upsert** is to replace the document if an document of the same id already exist; otherwise insert it.</span></span> <span data-ttu-id="f839d-195">Note ADF will automatically generate an id for the document if it is not specified either in the original doc or by column mapping), which means you need to make sure your document has an "id" so that upsert work as expected.</span><span class="sxs-lookup"><span data-stu-id="f839d-195">Note ADF will automatically generate an id for the document if it is not specified either in the original doc or by column mapping), which means you need to make sure your document has an "id" so that upsert work as expected.</span></span> |<span data-ttu-id="f839d-196">No, default is insert</span><span class="sxs-lookup"><span data-stu-id="f839d-196">No, default is insert</span></span> |
| <span data-ttu-id="f839d-197">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f839d-197">writeBatchSize</span></span> | <span data-ttu-id="f839d-198">Data Factory use [Cosmos DB bulk executor library](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) to write data into Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f839d-198">Data Factory use [Cosmos DB bulk executor library](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) to write data into Cosmos DB.</span></span> <span data-ttu-id="f839d-199">"writeBatchSize" controls the size of documents we provide to the library each time.</span><span class="sxs-lookup"><span data-stu-id="f839d-199">"writeBatchSize" controls the size of documents we provide to the library each time.</span></span> <span data-ttu-id="f839d-200">You can try increase writeBatchSize to improve performance.</span><span class="sxs-lookup"><span data-stu-id="f839d-200">You can try increase writeBatchSize to improve performance.</span></span> |<span data-ttu-id="f839d-201">No, default is 10,000</span><span class="sxs-lookup"><span data-stu-id="f839d-201">No, default is 10,000</span></span> |
| <span data-ttu-id="f839d-202">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="f839d-202">nestingSeparator</span></span> |<span data-ttu-id="f839d-203">A special character in the source column name to indicate that nested document is needed.</span><span class="sxs-lookup"><span data-stu-id="f839d-203">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="f839d-204">For example, `Name.First` in the output dataset structure generates the following JSON structure in the Cosmos DB document:`"Name": {"First": "[value maps to this column from source]"}` when the nestedSeparator is dot.</span><span class="sxs-lookup"><span data-stu-id="f839d-204">For example, `Name.First` in the output dataset structure generates the following JSON structure in the Cosmos DB document:`"Name": {"First": "[value maps to this column from source]"}` when the nestedSeparator is dot.</span></span> |<span data-ttu-id="f839d-205">No (default is dot `.`)</span><span class="sxs-lookup"><span data-stu-id="f839d-205">No (default is dot `.`)</span></span> |

<span data-ttu-id="f839d-206">**Example:**</span><span class="sxs-lookup"><span data-stu-id="f839d-206">**Example:**</span></span>

```json
"activities":[
    {
        "name": "CopyToCosmosDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Document DB output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "DocumentDbCollectionSink",
                "writeBehavior": "upsert"
            }
        }
    }
]
```

## <a name="importexport-json-documents"></a><span data-ttu-id="f839d-207">Import/Export JSON documents</span><span class="sxs-lookup"><span data-stu-id="f839d-207">Import/Export JSON documents</span></span>

<span data-ttu-id="f839d-208">Using this Cosmos DB connector, you can easily</span><span class="sxs-lookup"><span data-stu-id="f839d-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="f839d-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake Store, and other file-based stores supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f839d-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake Store, and other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="f839d-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span><span class="sxs-lookup"><span data-stu-id="f839d-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="f839d-211">Copy documents between two Cosmos DB collections as-is.</span><span class="sxs-lookup"><span data-stu-id="f839d-211">Copy documents between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="f839d-212">To achieve such schema-agnostic copy:</span><span class="sxs-lookup"><span data-stu-id="f839d-212">To achieve such schema-agnostic copy:</span></span>

* <span data-ttu-id="f839d-213">When using copy data tool, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span><span class="sxs-lookup"><span data-stu-id="f839d-213">When using copy data tool, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="f839d-214">When using activity authoring, do not specify the "structure" (aka schema) section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span><span class="sxs-lookup"><span data-stu-id="f839d-214">When using activity authoring, do not specify the "structure" (aka schema) section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="f839d-215">When importing from/exporting to JSON files, in the corresponding file store dataset, specify format type as "JsonFormat" and config "filePattern" properly (see [JSON format](supported-file-formats-and-compression-codecs.md#json-format) section for details), then do not specify the "structure" (aka schema) section and skip the rest format settings.</span><span class="sxs-lookup"><span data-stu-id="f839d-215">When importing from/exporting to JSON files, in the corresponding file store dataset, specify format type as "JsonFormat" and config "filePattern" properly (see [JSON format](supported-file-formats-and-compression-codecs.md#json-format) section for details), then do not specify the "structure" (aka schema) section and skip the rest format settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f839d-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="f839d-216">Next steps</span></span>
<span data-ttu-id="f839d-217">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f839d-217">For a list of data stores supported as sources and sinks by the copy activity in Azure Data Factory, see [supported data stores](copy-activity-overview.md##supported-data-stores-and-formats).</span></span>
