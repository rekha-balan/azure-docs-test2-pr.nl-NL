---
title: Move data to/from Azure Cosmos DB | Microsoft Docs
description: Learn how move data to/from Azure Cosmos DB collection using Azure Data Factory
services: data-factory, cosmosdb
documentationcenter: ''
author: linda33wj
manager: craigg
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: f3ebd704129aabecffdaa2589b8b086803a2d092
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870568"
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="e9310-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e9310-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-azure-documentdb-connector.md)
> * [Version 2 (current version)](../connector-azure-cosmos-db.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Azure Cosmos DB connector in V2](../connector-azure-cosmos-db.md).

<span data-ttu-id="e9310-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (SQL API).</span><span class="sxs-lookup"><span data-stu-id="e9310-108">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (SQL API).</span></span> <span data-ttu-id="e9310-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span><span class="sxs-lookup"><span data-stu-id="e9310-109">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="e9310-110">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="e9310-110">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="e9310-111">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="e9310-111">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> Azure Cosmos DB connector only supports the SQL API.

<span data-ttu-id="e9310-113">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="e9310-113">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="e9310-114">Getting started</span><span class="sxs-lookup"><span data-stu-id="e9310-114">Getting started</span></span>
<span data-ttu-id="e9310-115">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span><span class="sxs-lookup"><span data-stu-id="e9310-115">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="e9310-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span><span class="sxs-lookup"><span data-stu-id="e9310-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e9310-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span><span class="sxs-lookup"><span data-stu-id="e9310-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e9310-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span><span class="sxs-lookup"><span data-stu-id="e9310-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e9310-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span><span class="sxs-lookup"><span data-stu-id="e9310-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e9310-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span><span class="sxs-lookup"><span data-stu-id="e9310-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="e9310-121">Create **linked services** to link input and output data stores to your data factory.</span><span class="sxs-lookup"><span data-stu-id="e9310-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e9310-122">Create **datasets** to represent input and output data for the copy operation.</span><span class="sxs-lookup"><span data-stu-id="e9310-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="e9310-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="e9310-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e9310-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="e9310-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e9310-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span><span class="sxs-lookup"><span data-stu-id="e9310-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e9310-126">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span><span class="sxs-lookup"><span data-stu-id="e9310-126">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="e9310-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="e9310-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e9310-128">Linked service properties</span><span class="sxs-lookup"><span data-stu-id="e9310-128">Linked service properties</span></span>
<span data-ttu-id="e9310-129">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span><span class="sxs-lookup"><span data-stu-id="e9310-129">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="e9310-130">**Property**</span><span class="sxs-lookup"><span data-stu-id="e9310-130">**Property**</span></span> | <span data-ttu-id="e9310-131">**Description**</span><span class="sxs-lookup"><span data-stu-id="e9310-131">**Description**</span></span> | <span data-ttu-id="e9310-132">**Required**</span><span class="sxs-lookup"><span data-stu-id="e9310-132">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9310-133">type</span><span class="sxs-lookup"><span data-stu-id="e9310-133">type</span></span> |<span data-ttu-id="e9310-134">The type property must be set to: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="e9310-134">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="e9310-135">Yes</span><span class="sxs-lookup"><span data-stu-id="e9310-135">Yes</span></span> |
| <span data-ttu-id="e9310-136">connectionString</span><span class="sxs-lookup"><span data-stu-id="e9310-136">connectionString</span></span> |<span data-ttu-id="e9310-137">Specify information needed to connect to Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="e9310-137">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="e9310-138">Yes</span><span class="sxs-lookup"><span data-stu-id="e9310-138">Yes</span></span> |

<span data-ttu-id="e9310-139">Example:</span><span class="sxs-lookup"><span data-stu-id="e9310-139">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e9310-140">Dataset properties</span><span class="sxs-lookup"><span data-stu-id="e9310-140">Dataset properties</span></span>
<span data-ttu-id="e9310-141">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="e9310-141">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e9310-142">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span><span class="sxs-lookup"><span data-stu-id="e9310-142">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e9310-143">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span><span class="sxs-lookup"><span data-stu-id="e9310-143">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e9310-144">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span><span class="sxs-lookup"><span data-stu-id="e9310-144">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="e9310-145">**Property**</span><span class="sxs-lookup"><span data-stu-id="e9310-145">**Property**</span></span> | <span data-ttu-id="e9310-146">**Description**</span><span class="sxs-lookup"><span data-stu-id="e9310-146">**Description**</span></span> | <span data-ttu-id="e9310-147">**Required**</span><span class="sxs-lookup"><span data-stu-id="e9310-147">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9310-148">collectionName</span><span class="sxs-lookup"><span data-stu-id="e9310-148">collectionName</span></span> |<span data-ttu-id="e9310-149">Name of the Cosmos DB document collection.</span><span class="sxs-lookup"><span data-stu-id="e9310-149">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="e9310-150">Yes</span><span class="sxs-lookup"><span data-stu-id="e9310-150">Yes</span></span> |

<span data-ttu-id="e9310-151">Example:</span><span class="sxs-lookup"><span data-stu-id="e9310-151">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="e9310-152">Schema by Data Factory</span><span class="sxs-lookup"><span data-stu-id="e9310-152">Schema by Data Factory</span></span>
<span data-ttu-id="e9310-153">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="e9310-153">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="e9310-154">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span><span class="sxs-lookup"><span data-stu-id="e9310-154">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="e9310-155">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span><span class="sxs-lookup"><span data-stu-id="e9310-155">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="e9310-156">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span><span class="sxs-lookup"><span data-stu-id="e9310-156">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="e9310-157">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span><span class="sxs-lookup"><span data-stu-id="e9310-157">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="e9310-158">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span><span class="sxs-lookup"><span data-stu-id="e9310-158">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e9310-159">Copy activity properties</span><span class="sxs-lookup"><span data-stu-id="e9310-159">Copy activity properties</span></span>
<span data-ttu-id="e9310-160">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="e9310-160">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e9310-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span><span class="sxs-lookup"><span data-stu-id="e9310-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> The Copy Activity takes only one input and produces only one output.

<span data-ttu-id="e9310-163">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span><span class="sxs-lookup"><span data-stu-id="e9310-163">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="e9310-164">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="e9310-164">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e9310-165">**Property**</span><span class="sxs-lookup"><span data-stu-id="e9310-165">**Property**</span></span> | <span data-ttu-id="e9310-166">**Description**</span><span class="sxs-lookup"><span data-stu-id="e9310-166">**Description**</span></span> | <span data-ttu-id="e9310-167">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="e9310-167">**Allowed values**</span></span> | <span data-ttu-id="e9310-168">**Required**</span><span class="sxs-lookup"><span data-stu-id="e9310-168">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9310-169">query</span><span class="sxs-lookup"><span data-stu-id="e9310-169">query</span></span> |<span data-ttu-id="e9310-170">Specify the query to read data.</span><span class="sxs-lookup"><span data-stu-id="e9310-170">Specify the query to read data.</span></span> |<span data-ttu-id="e9310-171">Query string supported by Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e9310-171">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="e9310-172">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="e9310-172">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="e9310-173">No</span><span class="sxs-lookup"><span data-stu-id="e9310-173">No</span></span> <br/><br/><span data-ttu-id="e9310-174">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="e9310-174">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="e9310-175">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e9310-175">nestingSeparator</span></span> |<span data-ttu-id="e9310-176">Special character to indicate that the document is nested</span><span class="sxs-lookup"><span data-stu-id="e9310-176">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="e9310-177">Any character.</span><span class="sxs-lookup"><span data-stu-id="e9310-177">Any character.</span></span> <br/><br/><span data-ttu-id="e9310-178">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="e9310-178">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="e9310-179">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span><span class="sxs-lookup"><span data-stu-id="e9310-179">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="e9310-180">in the above examples.</span><span class="sxs-lookup"><span data-stu-id="e9310-180">in the above examples.</span></span> <span data-ttu-id="e9310-181">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="e9310-181">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="e9310-182">No</span><span class="sxs-lookup"><span data-stu-id="e9310-182">No</span></span> |

<span data-ttu-id="e9310-183">**DocumentDbCollectionSink** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="e9310-183">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="e9310-184">**Property**</span><span class="sxs-lookup"><span data-stu-id="e9310-184">**Property**</span></span> | <span data-ttu-id="e9310-185">**Description**</span><span class="sxs-lookup"><span data-stu-id="e9310-185">**Description**</span></span> | <span data-ttu-id="e9310-186">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="e9310-186">**Allowed values**</span></span> | <span data-ttu-id="e9310-187">**Required**</span><span class="sxs-lookup"><span data-stu-id="e9310-187">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9310-188">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e9310-188">nestingSeparator</span></span> |<span data-ttu-id="e9310-189">A special character in the source column name to indicate that nested document is needed.</span><span class="sxs-lookup"><span data-stu-id="e9310-189">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="e9310-190">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span><span class="sxs-lookup"><span data-stu-id="e9310-190">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="e9310-191">"Name": {</span><span class="sxs-lookup"><span data-stu-id="e9310-191">"Name": {</span></span><br/>    <span data-ttu-id="e9310-192">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="e9310-192">"First": "John"</span></span><br/><span data-ttu-id="e9310-193">},</span><span class="sxs-lookup"><span data-stu-id="e9310-193">},</span></span> |<span data-ttu-id="e9310-194">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="e9310-194">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="e9310-195">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="e9310-195">Default value is `.` (dot).</span></span> |<span data-ttu-id="e9310-196">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="e9310-196">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="e9310-197">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="e9310-197">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="e9310-198">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e9310-198">writeBatchSize</span></span> |<span data-ttu-id="e9310-199">Number of parallel requests to Azure Cosmos DB service to create documents.</span><span class="sxs-lookup"><span data-stu-id="e9310-199">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="e9310-200">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span><span class="sxs-lookup"><span data-stu-id="e9310-200">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="e9310-201">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span><span class="sxs-lookup"><span data-stu-id="e9310-201">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="e9310-202">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span><span class="sxs-lookup"><span data-stu-id="e9310-202">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="e9310-203">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span><span class="sxs-lookup"><span data-stu-id="e9310-203">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="e9310-204">Integer</span><span class="sxs-lookup"><span data-stu-id="e9310-204">Integer</span></span> |<span data-ttu-id="e9310-205">No (default: 5)</span><span class="sxs-lookup"><span data-stu-id="e9310-205">No (default: 5)</span></span> |
| <span data-ttu-id="e9310-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e9310-206">writeBatchTimeout</span></span> |<span data-ttu-id="e9310-207">Wait time for the operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="e9310-207">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="e9310-208">timespan</span><span class="sxs-lookup"><span data-stu-id="e9310-208">timespan</span></span><br/><br/> <span data-ttu-id="e9310-209">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="e9310-209">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e9310-210">No</span><span class="sxs-lookup"><span data-stu-id="e9310-210">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="e9310-211">Import/Export JSON documents</span><span class="sxs-lookup"><span data-stu-id="e9310-211">Import/Export JSON documents</span></span>
<span data-ttu-id="e9310-212">Using this Cosmos DB connector, you can easily</span><span class="sxs-lookup"><span data-stu-id="e9310-212">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="e9310-213">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e9310-213">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="e9310-214">Export JSON documents from Cosmos DB collecton into various file-based stores.</span><span class="sxs-lookup"><span data-stu-id="e9310-214">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="e9310-215">Migrate data between two Cosmos DB collections as-is.</span><span class="sxs-lookup"><span data-stu-id="e9310-215">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="e9310-216">To achieve such schema-agnostic copy,</span><span class="sxs-lookup"><span data-stu-id="e9310-216">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="e9310-217">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span><span class="sxs-lookup"><span data-stu-id="e9310-217">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="e9310-218">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span><span class="sxs-lookup"><span data-stu-id="e9310-218">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="e9310-219">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span><span class="sxs-lookup"><span data-stu-id="e9310-219">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="e9310-220">JSON examples</span><span class="sxs-lookup"><span data-stu-id="e9310-220">JSON examples</span></span>
<span data-ttu-id="e9310-221">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e9310-221">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e9310-222">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e9310-222">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="e9310-223">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e9310-223">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="e9310-224">Example: Copy data from Azure Cosmos DB to Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e9310-224">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="e9310-225">The sample below shows:</span><span class="sxs-lookup"><span data-stu-id="e9310-225">The sample below shows:</span></span>

1. <span data-ttu-id="e9310-226">A linked service of type [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-226">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="e9310-227">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-227">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e9310-228">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-228">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="e9310-229">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-229">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e9310-230">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-230">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e9310-231">The sample copies data in Azure Cosmos DB to Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="e9310-231">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="e9310-232">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="e9310-232">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e9310-233">**Azure Cosmos DB linked service:**</span><span class="sxs-lookup"><span data-stu-id="e9310-233">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="e9310-234">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="e9310-234">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="e9310-235">**Azure Document DB input dataset:**</span><span class="sxs-lookup"><span data-stu-id="e9310-235">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="e9310-236">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="e9310-236">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="e9310-237">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span><span class="sxs-lookup"><span data-stu-id="e9310-237">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e9310-238">**Azure Blob output dataset:**</span><span class="sxs-lookup"><span data-stu-id="e9310-238">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e9310-239">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span><span class="sxs-lookup"><span data-stu-id="e9310-239">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e9310-240">Sample JSON document in the Person collection in a Cosmos DB database:</span><span class="sxs-lookup"><span data-stu-id="e9310-240">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="e9310-241">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span><span class="sxs-lookup"><span data-stu-id="e9310-241">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="e9310-242">Example:</span><span class="sxs-lookup"><span data-stu-id="e9310-242">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="e9310-243">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="e9310-243">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="e9310-244">As part of the copy activity the input and output datasets have been specified.</span><span class="sxs-lookup"><span data-stu-id="e9310-244">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="e9310-245">Example: Copy data from Azure Blob to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e9310-245">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="e9310-246">The sample below shows:</span><span class="sxs-lookup"><span data-stu-id="e9310-246">The sample below shows:</span></span>

1. <span data-ttu-id="e9310-247">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-247">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="e9310-248">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-248">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e9310-249">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-249">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e9310-250">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-250">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="e9310-251">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="e9310-251">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="e9310-252">The sample copies data from Azure blob to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e9310-252">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="e9310-253">The JSON properties used in these samples are described in sections following the samples.</span><span class="sxs-lookup"><span data-stu-id="e9310-253">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e9310-254">**Azure Blob storage linked service:**</span><span class="sxs-lookup"><span data-stu-id="e9310-254">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="e9310-255">**Azure Cosmos DB linked service:**</span><span class="sxs-lookup"><span data-stu-id="e9310-255">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="e9310-256">**Azure Blob input dataset:**</span><span class="sxs-lookup"><span data-stu-id="e9310-256">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e9310-257">**Azure Cosmos DB output dataset:**</span><span class="sxs-lookup"><span data-stu-id="e9310-257">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="e9310-258">The sample copies data to a collection named “Person”.</span><span class="sxs-lookup"><span data-stu-id="e9310-258">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="e9310-259">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e9310-259">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="e9310-260">As part of the copy activity the input and output datasets have been specified.</span><span class="sxs-lookup"><span data-stu-id="e9310-260">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="e9310-261">If the sample blob input is as</span><span class="sxs-lookup"><span data-stu-id="e9310-261">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="e9310-262">Then the output JSON in Cosmos DB will be as:</span><span class="sxs-lookup"><span data-stu-id="e9310-262">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="e9310-263">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="e9310-263">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="e9310-264">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span><span class="sxs-lookup"><span data-stu-id="e9310-264">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="e9310-265">in this example.</span><span class="sxs-lookup"><span data-stu-id="e9310-265">in this example.</span></span> <span data-ttu-id="e9310-266">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="e9310-266">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="e9310-267">Appendix</span><span class="sxs-lookup"><span data-stu-id="e9310-267">Appendix</span></span>
1. <span data-ttu-id="e9310-268">**Question:** Does the Copy Activity support update of existing records?</span><span class="sxs-lookup"><span data-stu-id="e9310-268">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="e9310-269">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="e9310-269">**Answer:** No.</span></span>
2. <span data-ttu-id="e9310-270">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span><span class="sxs-lookup"><span data-stu-id="e9310-270">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="e9310-271">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span><span class="sxs-lookup"><span data-stu-id="e9310-271">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="e9310-272">**Question:** Does Data Factory support [range or hash-based data partitioning](../../cosmos-db/sql-api-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="e9310-272">**Question:** Does Data Factory support [range or hash-based data partitioning](../../cosmos-db/sql-api-partition-data.md)?</span></span>

    <span data-ttu-id="e9310-273">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="e9310-273">**Answer:** No.</span></span>
4. <span data-ttu-id="e9310-274">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span><span class="sxs-lookup"><span data-stu-id="e9310-274">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="e9310-275">**Answer:** No.</span><span class="sxs-lookup"><span data-stu-id="e9310-275">**Answer:** No.</span></span> <span data-ttu-id="e9310-276">Only one collection can be specified at this time.</span><span class="sxs-lookup"><span data-stu-id="e9310-276">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e9310-277">Performance and Tuning</span><span class="sxs-lookup"><span data-stu-id="e9310-277">Performance and Tuning</span></span>
<span data-ttu-id="e9310-278">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span><span class="sxs-lookup"><span data-stu-id="e9310-278">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
